---
layout: default
title: Publications
permalink: /publications/
---

# Publications
---

<div style="margin-bottom: 30px; padding-top: 10px;">
  View [
  <a href="#" id="filter-year" class="filter-link active">by year</a> : 
  <a href="#" id="filter-type" class="filter-link">by type</a> : 
  <a href="#" id="filter-all" class="filter-link">all (with superseded)</a>]
</div>

<div id="publications-container">
  <div id="books-list"></div>
  <div id="journal-articles-list"></div>
  <div id="conference-papers-list"></div>
  <div id="by-year-list" style="display: none;"></div>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/bibtex-parse-js@0.0.24/bibtexParse.min.js"></script>

<style>
.filter-link {
  text-decoration: none;
  color: #007bff;
  padding: 0;
}
.filter-link:hover {
  text-decoration: underline;
}
.filter-link.active {
  color: #00008B;
  cursor: default;
}
.filter-link.active:hover {
  text-decoration: none;
}
.superseded {
  opacity: 0.5;
  font-style: italic;
}
</style>

<script>
let allPublications = {
  books: [],
  journals: [],
  conferences: []
};

function loadBib(file, type) {
  return fetch(file)
    .then(response => response.text())
    .then(bibtex => {
      const parsed = bibtexParse.toJSON(bibtex);
      allPublications[type] = parsed;
    })
    .catch(error => {
      console.error(`Error loading ${file}:`, error);
    });
}

function renderByType() {
  renderSection(allPublications.books, 'books-list', 'Books/Book Chapters');
  renderSection(allPublications.journals, 'journal-articles-list', 'Journal Articles');
  renderSection(allPublications.conferences, 'conference-papers-list', 'Conference Papers');
  
  document.getElementById('by-year-list').style.display = 'none';
  document.getElementById('books-list').style.display = 'block';
  document.getElementById('journal-articles-list').style.display = 'block';
  document.getElementById('conference-papers-list').style.display = 'block';
}

function renderByYear() {
  const allPubs = [
    ...allPublications.books.map(p => ({...p, type: 'Book'})),
    ...allPublications.journals.map(p => ({...p, type: 'Journal Article'})),
    ...allPublications.conferences.map(p => ({...p, type: 'Conference Paper'}))
  ];

  // Sort by year descending
  allPubs.sort((a, b) => (b.entryTags.year || 0) - (a.entryTags.year || 0));

  // Group by year
  const byYear = {};
  allPubs.forEach(pub => {
    const year = pub.entryTags.year || 'Unknown';
    if (!byYear[year]) byYear[year] = [];
    byYear[year].push(pub);
  });

  let html = '';
  Object.keys(byYear).sort((a, b) => b - a).forEach(year => {
    html += `<h1>${year}</h1><ol>`;
    byYear[year].forEach(entry => {
      html += formatEntry(entry, true);
    });
    html += '</ol>';
  });

  document.getElementById('by-year-list').innerHTML = html;
  document.getElementById('by-year-list').style.display = 'block';
  document.getElementById('books-list').style.display = 'none';
  document.getElementById('journal-articles-list').style.display = 'none';
  document.getElementById('conference-papers-list').style.display = 'none';
}

function renderAll() {
  const allPubs = [
    ...allPublications.books.map(p => ({...p, type: 'Book'})),
    ...allPublications.journals.map(p => ({...p, type: 'Journal Article'})),
    ...allPublications.conferences.map(p => ({...p, type: 'Conference Paper'}))
  ];

  // Sort by year descending
  allPubs.sort((a, b) => (b.entryTags.year || 0) - (a.entryTags.year || 0));

  let html = '<h1>All Publications</h1><ol>';
  allPubs.forEach(entry => {
    html += formatEntry(entry, true, true);
  });
  html += '</ol>';

  document.getElementById('by-year-list').innerHTML = html;
  document.getElementById('by-year-list').style.display = 'block';
  document.getElementById('books-list').style.display = 'none';
  document.getElementById('journal-articles-list').style.display = 'none';
  document.getElementById('conference-papers-list').style.display = 'none';
}

function renderSection(data, containerId, sectionTitle) {
  const sorted = [...data].sort((a, b) => (b.entryTags.year || 0) - (a.entryTags.year || 0));
  
  let html = `<h1>${sectionTitle}</h1><ol>`;
  sorted.forEach(entry => {
    html += formatEntry(entry);
  });
  html += '</ol>';

  document.getElementById(containerId).innerHTML = html;
}

function formatEntry(entry, showType = false, showSuperseded = false) {
  const tags = entry.entryTags;
  const isSuperseded = tags.superseded === 'true' || tags.note?.toLowerCase().includes('superseded');
  
  let html = `<li style="margin-bottom: 20px;" class="${isSuperseded && showSuperseded ? 'superseded' : ''}">`;

  if (tags.author) html += `<strong>${tags.author}</strong>. `;
  if (tags.title) html += `"${tags.title}." `;
  if (tags.journal) html += `<em>${tags.journal}</em>`;
  else if (tags.booktitle) html += `<em>${tags.booktitle}</em>`;
  if (tags.volume) html += `, vol. ${tags.volume}`;
  if (tags.number) html += `, no. ${tags.number}`;
  if (tags.pages) html += `, pp. ${tags.pages}`;
  if (tags.year) html += `, ${tags.year}.`;
  
  // Add link based on view type
  if (tags.url) {
    if (showType && entry.type) {
      // In "by year" and "all" views: make the type a link
      html += ` <a href="${tags.url}" target="_blank">[${entry.type}]</a>`;
    } else {
      // In "by type" view: show [Link]
      html += ` <a href="${tags.url}" target="_blank">[Link]</a>`;
    }
  } else if (showType && entry.type) {
    // No URL but showing type: display type without link
    html += ` <span style="color: #666;">[${entry.type}]</span>`;
  }
  
  if (isSuperseded && showSuperseded) {
    html += ` <span style="color: #999;">(superseded)</span>`;
  }

  html += '</li>';
  return html;
}

// Load all files and set up filters
Promise.all([
  loadBib('{{ site.baseurl }}/assets/books.bib', 'books'),
  loadBib('{{ site.baseurl }}/assets/journal_articles.bib', 'journals'),
  loadBib('{{ site.baseurl }}/assets/conference_publications.bib', 'conferences')
]).then(() => {
  renderByYear()();
});

// Filter links
document.getElementById('filter-type').addEventListener('click', function(e) {
  e.preventDefault();
  document.querySelectorAll('.filter-link').forEach(l => l.classList.remove('active'));
  this.classList.add('active');
  renderByType();
});

document.getElementById('filter-year').addEventListener('click', function(e) {
  e.preventDefault();
  document.querySelectorAll('.filter-link').forEach(l => l.classList.remove('active'));
  this.classList.add('active');
  renderByYear();
});

document.getElementById('filter-all').addEventListener('click', function(e) {
  e.preventDefault();
  document.querySelectorAll('.filter-link').forEach(l => l.classList.remove('active'));
  this.classList.add('active');
  renderAll();
});
</script>
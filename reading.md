---
layout: post
title: "Tech Reading List"
permalink: /reading/
---

📚 A growing list of interesting academic literature. Want to add to your reading list? I recommend [__USENIX__](https://www.usenix.org/conferences/best-papers) and [__CHI__](https://programs.sigchi.org/chi/2026/awards/best-papers) papers to get started.

<!-- 1. Interactive Explorer Layout Container -->
<div class="explorer-wrapper">

  <!-- Filtering Control Panel: direct child of wrapper so grid-column spans both cols -->
  <div class="explorer-controls">
    <div class="control-group">
      <label>Category</label>
      <div class="segmented-control" id="category-filters">
        <button class="active" data-filter="All">All</button>
        <button data-filter="AI">AI</button>
        <button data-filter="Security">Security</button>
        <button data-filter="Systems">Systems</button>
        <button data-filter="HCI">HCI</button>
      </div>
    </div>
  </div>

  <!-- Left Side: Results Grid -->
  <div class="explorer-main">
    <div class="papers-grid" id="papers-grid">
      {% for paper in site.data.papers %}
      <div class="paper-card" 
           data-id="{{ paper.id }}"
           data-category="{{ paper.category }}" 
           tabindex="0">
        <div class="card-header">
          <span class="category-tag">{{ paper.category }}</span>
        </div>
        <h3 class="paper-title">{{ paper.title }}</h3>
        <p class="paper-summary-snippet">{{ paper.summary | truncate: 120 }}</p>
        <div class="keyword-pills">
          {% for keyword in paper.keywords %}
          <span class="pill">#{{ keyword }}</span>
          {% endfor %}
        </div>
        
        <!-- Hidden database payload used to populate details view dynamically -->
        <template class="paper-data">
          {
            "title": {{ paper.title | jsonify }},
            "category": {{ paper.category | jsonify }},
            "summary": {{ paper.summary | jsonify }},
            "matters": {{ paper.matters | jsonify }},
            "takeaway": {{ paper.takeaway | jsonify }},
            "link": {{ paper.link | jsonify }}
          }
        </template>
      </div>
      {% endfor %}
    </div>
  </div>

  <!-- Right Side: Sticky Detail Inspector Panel -->
  <aside class="explorer-inspector" id="explorer-inspector">
    <div class="inspector-placeholder" id="inspector-placeholder">
      <p>⬅️ Click on the literature in the list to see takeaways and where you can read it yourself.</p>
    </div>
    <div class="inspector-content hidden" id="inspector-content">
      <div class="inspector-header">
        <span class="inspector-category" id="ins-category"></span>
      </div>
      <h2 id="ins-title">Paper Title</h2>
      
      <div class="ins-section">
        <h4>Why it matters</h4>
        <p id="ins-matters"></p>
      </div>

      <div class="ins-section highlight-box">
        <h4>Key Takeaway</h4>
        <p id="ins-takeaway"></p>
      </div>

      <div class="ins-section">
        <h4>Summary</h4>
        <p id="ins-summary"></p>
      </div>

      <a id="ins-link" href="#" target="_blank" class="read-btn">Read The Literature &rarr;</a>
    </div>
  </aside>

</div>

<!-- 3. Explorer Scoped Stylesheets (Safely extends Moonwalk variables) -->
<style>
  :root {
    --accent-color: #0b57d0;
    --border-color: rgba(0, 0, 0, 0.08);
  }
  
  [data-theme="dark"] {
    --accent-color: #a8c7fa;
    --border-color: rgba(255, 255, 255, 0.1);
  }

  .explorer-wrapper {
    display: grid;
    grid-template-columns: 1fr 1.6fr;
    grid-template-rows: auto;
    gap: 1.5rem 2rem;
    align-items: start;
    margin-top: 1.5rem;
  }

  @media (max-width: 850px) {
    .explorer-wrapper {
      grid-template-columns: 1fr;
    }
  }

  /* Controls span both columns */
  .explorer-controls {
    grid-column: 1 / -1;
    display: flex;
    align-items: center;
    padding: 1rem 1.5rem;
    /* background: var(--bg-secondary, #fafafa); */
    border-radius: 8px;
    border: 2px solid var(--border-color);
  }

  .control-group {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    width: 100%;
  }

  .control-group label {
    font-size: 0.75rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-muted, #666);
  }

  .segmented-control {
    display: flex;
    gap: 4px;
    width: 100%;
    background: rgba(0, 0, 0, 0.04);
    padding: 4px;
    border-radius: 8px;
  }

  .segmented-control button {
    flex: 1;
    text-align: center;
    background: transparent;
    border: none;
    padding: 0.65rem 1.5rem;
    font-size: 1rem;
    font-weight: 700; /* was 500 */
    cursor: pointer;
    border-radius: 6px;
    color: var(--text, #333);
    transition: background 0.15s, color 0.15s, box-shadow 0.15s;
  }

  .segmented-control button:hover {
    background: rgba(255, 255, 255, 0.6);
  }

  .segmented-control button.active {
    background: var(--bg, #fff);
    color: var(--accent-color);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  }

  /* Papers Grid */
  .papers-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .paper-card {
    background: var(--bg-secondary, #fafafa);
    border: 1px solid var(--border-color);
    border-radius: 8px;
    padding: 1.25rem;
    cursor: pointer;
    transition: transform 0.15s ease, border-color 0.15s ease, box-shadow 0.15s ease;
  }

  .paper-card:hover {
    transform: translateY(-2px);
    border-color: var(--accent-color);
    box-shadow: 0 4px 12px rgba(0,0,0,0.03);
  }

  .paper-card.selected {
    border-color: var(--accent-color);
    background: rgba(11, 87, 208, 0.02);
  }

  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.5rem;
  }

  .category-tag {
    font-size: 0.75rem;
    font-weight: 500;
    opacity: 0.7;
  }

  .paper-title {
    margin: 0 0 0.5rem 0;
    font-size: 1.1rem;
    line-height: 1.3;
  }

  .paper-summary-snippet {
    font-size: 0.9rem;
    opacity: 0.8;
    margin-bottom: 1rem;
  }

  .keyword-pills {
    display: flex;
    flex-wrap: wrap;
    gap: 0.35rem;
  }

  .pill {
    font-size: 0.7rem;
    padding: 2px 6px;
    background: rgba(0,0,0,0.03);
    border-radius: 4px;
    opacity: 0.75;
  }

  /* Right Side Inspector */
  .explorer-inspector {
    position: sticky;
    top: 2rem;
    background: var(--bg-secondary, #fafafa);
    border: 1px solid var(--border-color);
    border-radius: 12px;
    padding: 1.5rem;
    min-height: 300px;
  }

  .inspector-placeholder {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 250px;
    text-align: center;
    color: var(--text-muted, #666);
    font-size: 0.9rem;
  }

  .inspector-header {
    display: flex;
    gap: 0.75rem;
    margin-bottom: 0.75rem;
  }

  .inspector-category {
    font-size: 0.75rem;
    font-weight: 600;
    background: var(--bg, #fff);
    border: 1px solid var(--border-color);
    padding: 2px 8px;
    border-radius: 99px;
  }

  .explorer-inspector h2 {
    margin-top: 0;
    font-size: 1.4rem;
    line-height: 1.25;
    margin-bottom: 1.5rem;
  }

  .ins-section {
    margin-bottom: 1.25rem;
  }

  .ins-section h4 {
    margin: 0 0 0.25rem 0;
    font-size: 0.75rem;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--text-muted, #666);
  }

  .ins-section p {
    margin: 0;
    font-size: 0.95rem;
    line-height: 1.45;
  }

  .highlight-box {
    background: var(--bg, #fff);
    border-left: 3px solid var(--accent-color);
    padding: 0.75rem;
    border-radius: 0 6px 6px 0;
  }

  .read-btn {
    display: inline-block;
    background: var(--accent-color);
    color: #fff !important;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 500;
    margin-top: 1rem;
    text-align: center;
    width: 80%;
  }

  .read-btn:hover {
    opacity: 0.9;
  }

  .hidden {
    display: none !important;
  }
</style>

<!-- 4. Interactive State Engine (Performant Vanilla JS) -->
<script>
  document.addEventListener("DOMContentLoaded", () => {
    const categoryContainer = document.getElementById("category-filters");
    const paperCards = document.querySelectorAll(".paper-card");
    
    // Inspector elements
    const placeholder = document.getElementById("inspector-placeholder");
    const content = document.getElementById("inspector-content");
    const insTitle = document.getElementById("ins-title");
    const insCategory = document.getElementById("ins-category");
    const insMatters = document.getElementById("ins-matters");
    const insTakeaway = document.getElementById("ins-takeaway");
    const insSummary = document.getElementById("ins-summary");
    const insLink = document.getElementById("ins-link");

    let currentCategory = "All";

    // Filter Logic
    const applyFilters = () => {
      paperCards.forEach(card => {
        const cat = card.getAttribute("data-category");
        const matchesCat = currentCategory === "All" || cat === currentCategory;

        if (matchesCat) {
          card.classList.remove("hidden");
        } else {
          card.classList.add("hidden");
          if (card.classList.contains("selected")) {
            clearSelection();
          }
        }
      });
    };

    // Category button handling
    categoryContainer.addEventListener("click", (e) => {
      const btn = e.target.closest("button");
      if (!btn) return;

      categoryContainer.querySelector("button.active").classList.remove("active");
      btn.classList.add("active");

      currentCategory = btn.getAttribute("data-filter");
      applyFilters();
    });

    // Selection Handling
    paperCards.forEach(card => {
      card.addEventListener("click", () => {
        // Manage active UI states
        const currentlySelected = document.querySelector(".paper-card.selected");
        if (currentlySelected) currentlySelected.classList.remove("selected");
        card.classList.add("selected");

        // Parse static JSON data payload from the template
        const rawData = card.querySelector(".paper-data").innerHTML;
        const data = JSON.parse(rawData);

        // Update Inspector details
        insTitle.textContent = data.title;
        insCategory.textContent = data.category;
        insMatters.textContent = data.matters;
        insTakeaway.textContent = data.takeaway;
        insSummary.textContent = data.summary;
        insLink.href = data.link;

        // Reveal content
        placeholder.classList.add("hidden");
        content.classList.remove("hidden");
      });

      // Accessibility: Allow keyboard selection
      card.addEventListener("keydown", (e) => {
        if (e.key === "Enter" || e.key === " ") {
          e.preventDefault();
          card.click();
        }
      });
    });

    function clearSelection() {
      const selected = document.querySelector(".paper-card.selected");
      if (selected) selected.classList.remove("selected");
      placeholder.classList.remove("hidden");
      content.classList.add("hidden");
    }
  });
</script>
---
layout: post
title: "Tech Reading List"
permalink: /reading/
---

📚 A growing list of interesting academic literature. Want to add to your reading list? I recommend [__USENIX__](https://www.usenix.org/conferences/best-papers) and [__CHI__](https://programs.sigchi.org/chi/2026/awards/best-papers) papers to get started.

<div class="explorer-wrapper">

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

  <div class="explorer-main">
    <div class="papers-grid" id="papers-grid">
      {% for paper in site.data.papers %}
      <div class="paper-card"
           data-id="{{ paper.id }}"
           data-category="{{ paper.category }}"
           tabindex="0">
        <div class="card-header">
          <span class="category-tag">{{ paper.category }}</span>
          <span class="card-chevron" aria-hidden="true">›</span>
        </div>
        <h3 class="paper-title">{{ paper.title }}</h3>
        <div class="keyword-pills">
          {% for keyword in paper.keywords %}
          <span class="pill">#{{ keyword }}</span>
          {% endfor %}
        </div>

        <!-- Inline expanded detail -->
        <div class="card-expanded-detail">
          <div class="card-divider"></div>
          <p class="paper-summary-snippet exp-snippet"></p>
          <div class="ins-section highlight-box">
            <h4>Key Takeaway</h4>
            <p class="exp-takeaway"></p>
          </div>
          <div class="ins-section">
            <h4>Summary</h4>
            <p class="exp-summary"></p>
          </div>
          <a class="exp-link read-btn" href="#" target="_blank">Read The Literature &rarr;</a>
        </div>

        <template class="paper-data">
          {
            "title": {{ paper.title | jsonify }},
            "category": {{ paper.category | jsonify }},
            "summary": {{ paper.summary | jsonify }},
            "takeaway": {{ paper.takeaway | jsonify }},
            "link": {{ paper.link | jsonify }}
          }
        </template>
      </div>
      {% endfor %}
    </div>
  </div>

</div>

<style>
  :root {
    --accent-color: #0b57d0;
    --border-color: rgba(0, 0, 0, 0.08);
  }

  [data-theme="dark"] {
    --accent-color: #a8c7fa;
    --border-color: rgba(255, 255, 255, 0.1);
  }

  /* Single-column layout — no inspector panel */
  .explorer-wrapper {
    display: flex;
    flex-direction: column;
    gap: 1.5rem;
    margin-top: 1.5rem;
  }

  .explorer-controls {
    display: flex;
    align-items: center;
    padding: 1rem 1.5rem;
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
    font-weight: 700;
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

  /* Full-width card grid */
  .papers-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 0.6rem;
  }

  /* Compact card — roughly half the original height */
  .paper-card {
    background: var(--bg-secondary, #fafafa);
    border: 1px solid var(--border-color);
    border-radius: 8px;
    padding: 0.75rem 1rem;
    cursor: pointer;
    transition: border-color 0.15s ease, box-shadow 0.15s ease;
  }

  .paper-card:hover {
    border-color: var(--accent-color);
    box-shadow: 0 2px 8px rgba(0,0,0,0.04);
  }

  .paper-card.selected {
    border-color: var(--accent-color);
    background: rgba(11, 87, 208, 0.02);
  }

  .card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 0.3rem;
  }

  .category-tag {
    font-size: 0.75rem;
    font-weight: 500;
    opacity: 0.7;
  }

  .card-chevron {
    font-size: 1.2rem;
    color: var(--accent-color);
    transition: transform 0.25s ease;
    line-height: 1;
  }

  .paper-card.expanded .card-chevron {
    transform: rotate(90deg);
  }

  .paper-title {
    margin: 0 0 0.4rem 0;
    font-size: 1rem;
    line-height: 1.3;
  }

  .keyword-pills {
    display: flex;
    flex-wrap: wrap;
    gap: 0.3rem;
  }

  .pill {
    font-size: 0.7rem;
    padding: 2px 6px;
    background: rgba(0,0,0,0.03);
    border-radius: 4px;
    opacity: 0.75;
  }

  /* Expanded inline detail */
  .card-expanded-detail {
    display: none;
  }

  .paper-card.expanded .card-expanded-detail {
    display: block;
  }

  .card-divider {
    height: 1px;
    background: var(--border-color);
    margin: 0.85rem 0;
  }

  .paper-summary-snippet {
    font-size: 0.9rem;
    opacity: 0.8;
    margin: 0 0 1rem 0;
  }

  .ins-section {
    margin-bottom: 1.1rem;
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
    margin-top: 0.5rem;
    text-align: center;
    width: 80%;
  }

  .read-btn:hover {
    opacity: 0.9;
  }

  .hidden {
    display: none !important;
  }

  /* ── Mobile: fix segmented control overflow ── */
  @media (max-width: 600px) {
    .explorer-controls {
      padding: 0.75rem 1rem;
    }

    .segmented-control {
      flex-wrap: wrap;
    }

    .segmented-control button {
      flex: 1 1 auto;
      padding: 0.5rem 0.75rem;
      font-size: 0.875rem;
    }
  }

  /* ── Very small phones (375px and below) ── */
  @media (max-width: 375px) {
    .segmented-control button {
      padding: 0.45rem 0.5rem;
      font-size: 0.8rem;
    }
  }
</style>

<script>
  document.addEventListener("DOMContentLoaded", () => {
    const categoryContainer = document.getElementById("category-filters");
    const paperCards = document.querySelectorAll(".paper-card");

    let currentCategory = "All";

    // ── Filter logic ──
    const applyFilters = () => {
      paperCards.forEach(card => {
        const cat = card.getAttribute("data-category");
        const matches = currentCategory === "All" || cat === currentCategory;
        if (matches) {
          card.classList.remove("hidden");
        } else {
          card.classList.add("hidden");
          card.classList.remove("expanded", "selected");
        }
      });
    };

    categoryContainer.addEventListener("click", (e) => {
      const btn = e.target.closest("button");
      if (!btn) return;
      categoryContainer.querySelector("button.active").classList.remove("active");
      btn.classList.add("active");
      currentCategory = btn.getAttribute("data-filter");
      applyFilters();
    });

    // ── Card expand/collapse ──
    paperCards.forEach(card => {
      card.addEventListener("click", () => {
        const rawData = card.querySelector(".paper-data").innerHTML;
        const data = JSON.parse(rawData);
        const isAlreadyExpanded = card.classList.contains("expanded");

        // Collapse any open card
        document.querySelectorAll(".paper-card.expanded").forEach(c => {
          c.classList.remove("expanded", "selected");
        });

        if (!isAlreadyExpanded) {
          card.classList.add("expanded", "selected");

          const detail = card.querySelector(".card-expanded-detail");
          detail.querySelector(".exp-takeaway").textContent = data.takeaway;
          detail.querySelector(".exp-summary").textContent = data.summary;
          detail.querySelector(".exp-link").href = data.link;
        }
      });

      card.addEventListener("keydown", (e) => {
        if (e.key === "Enter" || e.key === " ") {
          e.preventDefault();
          card.click();
        }
      });
    });
  });
</script>

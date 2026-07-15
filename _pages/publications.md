---
layout: page
permalink: /publications/
title: publications
titledisplay: publications
description: (*) denotes equal contribution
nav: true
nav_order: 2
---

<p class="pubs-lead">
  See the full list on
  <a href="https://scholar.google.com/citations?user=seUq_d0AAAAJ&amp;hl=en" target="_blank" rel="noopener">Google Scholar</a>.
</p>

<div class="pub-sort" role="group" aria-label="Sort publications">
  <button type="button" class="pub-sort__btn is-active" data-sort="year" aria-pressed="true">By year</button>
  <button type="button" class="pub-sort__btn" data-sort="topic" aria-pressed="false">By topic</button>
</div>

<div class="publications" id="pubs-by-year">
{% bibliography %}
</div>

<div class="publications" id="pubs-by-topic" hidden></div>

<script>
  (function () {
    var byYear = document.getElementById("pubs-by-year");
    var byTopic = document.getElementById("pubs-by-topic");
    if (!byYear || !byTopic) return;

    // Group the year-sorted entries by their topic (bibtex `class` field),
    // preserving first-appearance order (i.e. newest-first within each topic).
    var entries = byYear.querySelectorAll("ol.bibliography > li");
    var order = [];
    var buckets = {};
    Array.prototype.forEach.call(entries, function (li) {
      var el = li.querySelector("[data-topic]");
      var topic = el && el.getAttribute("data-topic");
      topic = topic && topic.trim() ? topic.trim() : "Other";
      if (!buckets[topic]) {
        buckets[topic] = [];
        order.push(topic);
      }
      buckets[topic].push(li);
    });

    order.forEach(function (topic) {
      var h2 = document.createElement("h2");
      h2.className = "bibliography";
      h2.textContent = topic;
      byTopic.appendChild(h2);

      var ol = document.createElement("ol");
      ol.className = "bibliography";
      buckets[topic].forEach(function (li) {
        var clone = li.cloneNode(true);
        // Avoid duplicate element IDs across the two views.
        Array.prototype.forEach.call(clone.querySelectorAll("[id]"), function (n) {
          n.removeAttribute("id");
        });
        ol.appendChild(clone);
      });
      byTopic.appendChild(ol);
    });

    var btns = document.querySelectorAll(".pub-sort__btn");
    Array.prototype.forEach.call(btns, function (btn) {
      btn.addEventListener("click", function () {
        var showTopic = btn.getAttribute("data-sort") === "topic";
        Array.prototype.forEach.call(btns, function (b) {
          var active = b === btn;
          b.classList.toggle("is-active", active);
          b.setAttribute("aria-pressed", active ? "true" : "false");
        });
        byTopic.hidden = !showTopic;
        byYear.hidden = showTopic;
      });
    });
  })();
</script>

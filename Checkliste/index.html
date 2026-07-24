/* =========================================================
   Steuer Checkliste — Application Logic
   Vanilla JavaScript, no framework, no build step.
   ========================================================= */

(function () {
  'use strict';

  /* ---------------------------------------------------------
     1. DATA — Checklist categories and tasks (German content)
     --------------------------------------------------------- */
  const CHECKLIST_DATA = [
    {
      id: 'personal',
      icon: 'user',
      title: 'Persönliche Unterlagen',
      tasks: [
        'Personalausweis oder Reisepass (Kopie)',
        'Steuerliche Identifikationsnummer',
        'IBAN für die Erstattung',
        'Änderungen der Anschrift im Steuerjahr',
        'Nachweis über Änderung des Familienstands',
        'Kirchensteuer-Zugehörigkeit prüfen'
      ]
    },
    {
      id: 'employment',
      icon: 'briefcase',
      title: 'Arbeitsunterlagen',
      tasks: [
        'Lohnsteuerbescheinigung des Arbeitgebers',
        'Letzte Gehaltsabrechnung des Jahres',
        'Nachweise über Abfindungen oder Sonderzahlungen',
        'Arbeitsvertrag bei neuem Arbeitgeber',
        'Bescheinigungen zu Fortbildungen',
        'Reisekostenabrechnungen',
        'Nachweis über Kurzarbeitergeld (falls zutreffend)'
      ]
    },
    {
      id: 'commute',
      icon: 'car',
      title: 'Pendlerpauschale',
      tasks: [
        'Anzahl der Arbeitstage im Büro',
        'Entfernung zwischen Wohnung und erster Tätigkeitsstätte',
        'Nachweise über ÖPNV-Nutzung (z. B. Jahreskarte)',
        'Nachweise zur Fahrgemeinschaft',
        'Tankquittungen bei Nutzung des eigenen Fahrzeugs',
        'Nachweis über Fahrrad- oder Motorradnutzung'
      ]
    },
    {
      id: 'homeoffice',
      icon: 'home',
      title: 'Home Office',
      tasks: [
        'Anzahl der Home-Office-Tage im Jahr',
        'Nachweis für die Home-Office-Pauschale',
        'Größe des separaten Arbeitszimmers (falls vorhanden)',
        'Anteilige Nebenkosten der Wohnung',
        'Beruflich genutzte Internet- und Telefonkosten',
        'Anteilige Stromkosten'
      ]
    },
    {
      id: 'equipment',
      icon: 'laptop',
      title: 'Arbeitsmittel',
      tasks: [
        'Rechnungen für Laptop oder PC',
        'Rechnungen für Bürostuhl und Schreibtisch',
        'Belege für Fachliteratur',
        'Rechnungen für Software-Lizenzen',
        'Nachweise über beruflich genutztes Telefon',
        'Belege für Arbeits- oder Berufskleidung'
      ]
    },
    {
      id: 'insurance',
      icon: 'shield',
      title: 'Versicherungen',
      tasks: [
        'Beitragsnachweis Haftpflichtversicherung',
        'Beitragsnachweis Berufsunfähigkeitsversicherung',
        'Beitragsnachweis Krankenversicherung',
        'Beitragsnachweis Rentenversicherung',
        'Beitragsnachweis Unfallversicherung',
        'Beitragsnachweis Risikolebensversicherung'
      ]
    },
    {
      id: 'donations',
      icon: 'heart-handshake',
      title: 'Spenden',
      tasks: [
        'Spendenquittungen gemeinnütziger Organisationen',
        'Nachweise über Mitgliedsbeiträge',
        'Nachweise über Parteispenden',
        'Nachweise über Sachspenden',
        'Nachweise über Spenden an die Kirche'
      ]
    },
    {
      id: 'family',
      icon: 'users',
      title: 'Familie',
      tasks: [
        'Nachweise über Kindergeld',
        'Belege für Kinderbetreuungskosten',
        'Nachweise über Schulgeld',
        'Nachweise über Unterhaltszahlungen',
        'Steuerdaten des Ehe- oder Lebenspartners',
        'Elterngeldbescheid'
      ]
    },
    {
      id: 'investments',
      icon: 'trending-up',
      title: 'Kapitalanlagen',
      tasks: [
        'Jahressteuerbescheinigung der Bank',
        'Freistellungsauftrag prüfen und aktualisieren',
        'Verlustbescheinigung des Depots',
        'Zinsbescheinigungen',
        'Dividendenabrechnungen',
        'Übersicht über Kryptowährungs-Transaktionen'
      ]
    },
    {
      id: 'final',
      icon: 'clipboard-check',
      title: 'Abschlusskontrolle',
      tasks: [
        'Alle Belege chronologisch sortiert',
        'Steuerbescheid des Vorjahres griffbereit',
        'ELSTER-Zugang aktiv und Zertifikat gültig',
        'Abgabefrist geprüft',
        'Rücksprache mit Steuerberater gehalten (falls nötig)',
        'Checkliste vollständig durchgegangen',
        'Checkliste als PDF exportiert und gesichert'
      ]
    }
  ];

  /* ---------------------------------------------------------
     2. STATE
     --------------------------------------------------------- */
  const STORAGE_KEYS = {
    tasks: 'steuerChecklist.tasks',
    notes: 'steuerChecklist.notes',
    notesTimestamp: 'steuerChecklist.notesTimestamp',
    theme: 'steuerChecklist.theme',
    openCategories: 'steuerChecklist.openCategories'
  };

  const TOTAL_TASKS = CHECKLIST_DATA.reduce((sum, cat) => sum + cat.tasks.length, 0);
  const CIRCUMFERENCE = 2 * Math.PI * 58; // matches SVG circle r=58

  let taskState = loadJSON(STORAGE_KEYS.tasks, {});
  let openCategories = loadJSON(STORAGE_KEYS.openCategories, {});
  let hasCelebrated = false;
  let toastTimer = null;
  let notesSaveTimer = null;

  function loadJSON(key, fallback) {
    try {
      const raw = localStorage.getItem(key);
      return raw ? JSON.parse(raw) : fallback;
    } catch (err) {
      console.warn('Konnte gespeicherte Daten nicht laden:', key, err);
      return fallback;
    }
  }

  function saveJSON(key, value) {
    try {
      localStorage.setItem(key, JSON.stringify(value));
    } catch (err) {
      console.warn('Konnte Daten nicht speichern:', key, err);
    }
  }

  function taskKey(categoryId, index) {
    return categoryId + '::' + index;
  }

  /* ---------------------------------------------------------
     3. DOM REFERENCES
     --------------------------------------------------------- */
  const el = {
    checklist: document.getElementById('checklist'),
    noResults: document.getElementById('noResults'),
    progressPercent: document.getElementById('progressPercent'),
    progressSummary: document.getElementById('progressSummary'),
    progressBarFill: document.getElementById('progressBarFill'),
    progressBarOuter: document.getElementById('progressBarOuter'),
    progressRingValue: document.getElementById('progressRingValue'),
    progressCard: document.getElementById('progressCard'),
    progressEta: document.getElementById('progressEta'),
    statCompleted: document.getElementById('statCompleted'),
    statOpen: document.getElementById('statOpen'),
    statTotal: document.getElementById('statTotal'),
    darkModeToggle: document.getElementById('darkModeToggle'),
    searchToggle: document.getElementById('searchToggle'),
    searchBar: document.getElementById('searchBar'),
    searchInput: document.getElementById('searchInput'),
    searchClear: document.getElementById('searchClear'),
    searchResultCount: document.getElementById('searchResultCount'),
    expandAllBtn: document.getElementById('expandAllBtn'),
    exportPdfBtn: document.getElementById('exportPdfBtn'),
    resetBtn: document.getElementById('resetBtn'),
    resetModalOverlay: document.getElementById('resetModalOverlay'),
    resetCancelBtn: document.getElementById('resetCancelBtn'),
    resetConfirmBtn: document.getElementById('resetConfirmBtn'),
    notesTextarea: document.getElementById('notesTextarea'),
    notesCharCount: document.getElementById('notesCharCount'),
    notesTimestamp: document.getElementById('notesTimestamp'),
    ctaStart: document.getElementById('ctaStart'),
    toast: document.getElementById('toast'),
    toastMessage: document.getElementById('toastMessage'),
    footerYear: document.getElementById('footerYear'),
    confettiCanvas: document.getElementById('confettiCanvas')
  };

  /* ---------------------------------------------------------
     4. RENDER CHECKLIST
     --------------------------------------------------------- */
  function renderChecklist() {
    const fragment = document.createDocumentFragment();

    CHECKLIST_DATA.forEach((category, catIndex) => {
      const card = document.createElement('article');
      card.className = 'category-card';
      card.dataset.categoryId = category.id;
      card.style.animationDelay = (catIndex * 40) + 'ms';

      const isOpen = !!openCategories[category.id];
      if (isOpen) card.classList.add('is-open');

      const headerId = 'cat-header-' + category.id;
      const bodyId = 'cat-body-' + category.id;

      card.innerHTML =
        '<button class="category-card__header" id="' + headerId + '" ' +
          'aria-expanded="' + isOpen + '" aria-controls="' + bodyId + '" type="button">' +
          '<span class="category-card__icon"><i data-lucide="' + category.icon + '" aria-hidden="true"></i></span>' +
          '<span class="category-card__heading">' +
            '<span class="category-card__title">' + category.title + '</span>' +
            '<span class="category-card__meta">' + category.tasks.length + ' Aufgaben</span>' +
          '</span>' +
          '<span class="category-card__badge" data-role="badge">0 / ' + category.tasks.length + '</span>' +
          '<i data-lucide="chevron-down" class="category-card__chevron" aria-hidden="true"></i>' +
        '</button>' +
        '<div class="category-card__body" id="' + bodyId + '" role="region" aria-labelledby="' + headerId + '">' +
          '<div class="category-card__body-inner">' +
            '<ul class="task-list" data-role="task-list"></ul>' +
          '</div>' +
        '</div>';

      const taskList = card.querySelector('[data-role="task-list"]');

      category.tasks.forEach((taskText, taskIndex) => {
        const key = taskKey(category.id, taskIndex);
        const checked = !!taskState[key];
        const inputId = 'task-' + category.id + '-' + taskIndex;

        const li = document.createElement('li');
        li.className = 'task-item';
        li.dataset.taskText = taskText.toLowerCase();

        li.innerHTML =
          '<span class="task-checkbox">' +
            '<input type="checkbox" id="' + inputId + '" ' + (checked ? 'checked' : '') + ' ' +
              'data-category="' + category.id + '" data-index="' + taskIndex + '">' +
            '<span class="task-checkbox__box">' +
              '<i data-lucide="check" aria-hidden="true"></i>' +
            '</span>' +
          '</span>' +
          '<label class="task-item__label" for="' + inputId + '">' +
            '<span class="task-item__text">' + taskText + '</span>' +
          '</label>';

        taskList.appendChild(li);
      });

      // Header click toggles open/closed
      const headerBtn = card.querySelector('.category-card__header');
      headerBtn.addEventListener('click', () => toggleCategory(card, category.id));

      fragment.appendChild(card);
    });

    el.checklist.innerHTML = '';
    el.checklist.appendChild(fragment);

    // Attach checkbox listeners (event delegation would also work, direct is fine here)
    el.checklist.querySelectorAll('input[type="checkbox"]').forEach((input) => {
      input.addEventListener('change', onTaskToggle);
    });

    refreshIcons();
    updateAllBadges();
    updateProgress();
  }

  function toggleCategory(card, categoryId) {
    const isOpen = card.classList.toggle('is-open');
    const header = card.querySelector('.category-card__header');
    header.setAttribute('aria-expanded', String(isOpen));
    openCategories[categoryId] = isOpen;
    saveJSON(STORAGE_KEYS.openCategories, openCategories);
  }

  function onTaskToggle(event) {
    const input = event.target;
    const categoryId = input.dataset.category;
    const index = input.dataset.index;
    const key = taskKey(categoryId, index);

    taskState[key] = input.checked;
    saveJSON(STORAGE_KEYS.tasks, taskState);

    updateCategoryBadge(categoryId);
    updateProgress();
    showToast('Automatisch gespeichert');
  }

  function updateAllBadges() {
    CHECKLIST_DATA.forEach((category) => updateCategoryBadge(category.id));
  }

  function updateCategoryBadge(categoryId) {
    const category = CHECKLIST_DATA.find((c) => c.id === categoryId);
    if (!category) return;

    const card = el.checklist.querySelector('[data-category-id="' + categoryId + '"]');
    if (!card) return;

    const badge = card.querySelector('[data-role="badge"]');
    let completed = 0;
    category.tasks.forEach((_, idx) => {
      if (taskState[taskKey(categoryId, idx)]) completed++;
    });

    badge.textContent = completed + ' / ' + category.tasks.length;
    badge.dataset.state = completed === 0 ? 'empty' : (completed === category.tasks.length ? 'complete' : 'partial');
  }

  /* ---------------------------------------------------------
     5. PROGRESS CALCULATION
     --------------------------------------------------------- */
  function getCompletedCount() {
    return Object.values(taskState).filter(Boolean).length;
  }

  function updateProgress() {
    const completed = Math.min(getCompletedCount(), TOTAL_TASKS);
    const remaining = TOTAL_TASKS - completed;
    const percent = TOTAL_TASKS === 0 ? 0 : Math.round((completed / TOTAL_TASKS) * 100);

    el.progressPercent.textContent = percent + '%';
    el.progressSummary.textContent = completed + ' von ' + TOTAL_TASKS + ' erledigt';
    el.progressBarFill.style.width = percent + '%';
    el.progressBarOuter.setAttribute('aria-valuenow', String(percent));

    el.statCompleted.textContent = String(completed);
    el.statOpen.textContent = String(remaining);
    el.statTotal.textContent = String(TOTAL_TASKS);

    const offset = CIRCUMFERENCE - (percent / 100) * CIRCUMFERENCE;
    el.progressRingValue.style.strokeDashoffset = String(offset);

    if (percent >= 100) {
      el.progressRingValue.style.stroke = 'var(--color-success)';
    } else {
      el.progressRingValue.style.stroke = 'var(--color-brand)';
    }

    // Estimated completion hint
    if (remaining === 0 && TOTAL_TASKS > 0) {
      el.progressEta.textContent = 'Alle Unterlagen vollständig — bereit zur Abgabe!';
    } else if (completed === 0) {
      el.progressEta.textContent = 'Noch keine Aufgabe erledigt. Legen Sie los!';
    } else {
      el.progressEta.textContent = 'Noch ' + remaining + ' Aufgabe' + (remaining === 1 ? '' : 'n') + ' bis zur vollständigen Checkliste.';
    }

    if (percent >= 100 && !hasCelebrated) {
      hasCelebrated = true;
      launchConfetti();
    } else if (percent < 100) {
      hasCelebrated = false;
    }
  }

  /* ---------------------------------------------------------
     6. DARK MODE
     --------------------------------------------------------- */
  function initTheme() {
    const saved = localStorage.getItem(STORAGE_KEYS.theme);
    const prefersDark = window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches;
    const theme = saved || (prefersDark ? 'dark' : 'light');
    applyTheme(theme);
  }

  function applyTheme(theme) {
    if (theme === 'dark') {
      document.documentElement.setAttribute('data-theme', 'dark');
      el.darkModeToggle.setAttribute('aria-pressed', 'true');
      el.darkModeToggle.innerHTML = '<i data-lucide="sun" aria-hidden="true"></i> Hellmodus';
    } else {
      document.documentElement.removeAttribute('data-theme');
      el.darkModeToggle.setAttribute('aria-pressed', 'false');
      el.darkModeToggle.innerHTML = '<i data-lucide="moon" aria-hidden="true"></i> Dunkelmodus';
    }
    refreshIcons();
    saveJSON(STORAGE_KEYS.theme, theme);
    localStorage.setItem(STORAGE_KEYS.theme, theme);
  }

  function toggleTheme() {
    const isDark = document.documentElement.getAttribute('data-theme') === 'dark';
    applyTheme(isDark ? 'light' : 'dark');
  }

  /* ---------------------------------------------------------
     7. SEARCH
     --------------------------------------------------------- */
  function toggleSearchBar() {
    const isHidden = el.searchBar.hidden;
    el.searchBar.hidden = !isHidden;
    el.searchToggle.setAttribute('aria-expanded', String(isHidden));
    if (isHidden) {
      el.searchInput.focus();
    } else {
      clearSearch();
    }
  }

  function clearSearch() {
    el.searchInput.value = '';
    el.searchClear.hidden = true;
    el.searchResultCount.textContent = '';
    applySearchFilter('');
  }

  function applySearchFilter(rawQuery) {
    const query = rawQuery.trim().toLowerCase();
    let visibleCount = 0;
    let anyCategoryVisible = false;

    const cards = el.checklist.querySelectorAll('.category-card');
    cards.forEach((card) => {
      const items = card.querySelectorAll('.task-item');
      let categoryHasMatch = false;

      items.forEach((item) => {
        const text = item.dataset.taskText || '';
        const matches = query === '' || text.includes(query);
        item.classList.toggle('is-hidden', !matches);

        const textSpan = item.querySelector('.task-item__text');
        if (matches && query !== '') {
          textSpan.innerHTML = highlightMatch(textSpan.textContent, query);
          categoryHasMatch = true;
          visibleCount++;
        } else {
          textSpan.innerHTML = textSpan.textContent;
          if (matches) visibleCount++;
        }
      });

      const shouldShowCard = query === '' || categoryHasMatch;
      card.hidden = !shouldShowCard;
      if (shouldShowCard) anyCategoryVisible = true;

      if (query !== '' && categoryHasMatch && !card.classList.contains('is-open')) {
        card.classList.add('is-open');
        card.querySelector('.category-card__header').setAttribute('aria-expanded', 'true');
      }
    });

    el.noResults.hidden = anyCategoryVisible;

    if (query === '') {
      el.searchResultCount.textContent = '';
    } else {
      el.searchResultCount.textContent = visibleCount + ' Ergebnis' + (visibleCount === 1 ? '' : 'se') + ' gefunden';
    }
  }

  function highlightMatch(text, query) {
    const escaped = query.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
    const regex = new RegExp('(' + escaped + ')', 'ig');
    return text.replace(regex, '<mark>$1</mark>');
  }

  /* ---------------------------------------------------------
     8. EXPAND / COLLAPSE ALL
     --------------------------------------------------------- */
  function toggleExpandAll() {
    const cards = Array.from(el.checklist.querySelectorAll('.category-card'));
    const allOpen = cards.every((card) => card.classList.contains('is-open'));
    const nextState = !allOpen;

    cards.forEach((card) => {
      card.classList.toggle('is-open', nextState);
      card.querySelector('.category-card__header').setAttribute('aria-expanded', String(nextState));
      openCategories[card.dataset.categoryId] = nextState;
    });

    saveJSON(STORAGE_KEYS.openCategories, openCategories);

    el.expandAllBtn.innerHTML = nextState
      ? '<i data-lucide="chevrons-up-down" aria-hidden="true"></i> Alle einklappen'
      : '<i data-lucide="chevrons-down-up" aria-hidden="true"></i> Alle aufklappen';
    refreshIcons();
  }

  /* ---------------------------------------------------------
     9. NOTES (auto-save + character counter)
     --------------------------------------------------------- */
  function initNotes() {
    const savedNotes = localStorage.getItem(STORAGE_KEYS.notes) || '';
    el.notesTextarea.value = savedNotes;
    updateCharCount();

    const savedTimestamp = localStorage.getItem(STORAGE_KEYS.notesTimestamp);
    if (savedTimestamp) {
      el.notesTimestamp.textContent = 'Zuletzt gespeichert: ' + savedTimestamp;
    }

    el.notesTextarea.addEventListener('input', () => {
      updateCharCount();
      clearTimeout(notesSaveTimer);
      notesSaveTimer = setTimeout(saveNotes, 600);
    });
  }

  function updateCharCount() {
    el.notesCharCount.textContent = el.notesTextarea.value.length + ' / 4000 Zeichen';
  }

  function saveNotes() {
    localStorage.setItem(STORAGE_KEYS.notes, el.notesTextarea.value);
    const now = new Date();
    const timestamp = now.toLocaleDateString('de-DE') + ', ' + now.toLocaleTimeString('de-DE', { hour: '2-digit', minute: '2-digit' });
    localStorage.setItem(STORAGE_KEYS.notesTimestamp, timestamp);
    el.notesTimestamp.textContent = 'Zuletzt gespeichert: ' + timestamp;
    showToast('Notizen automatisch gespeichert');
  }

  /* ---------------------------------------------------------
     10. RESET
     --------------------------------------------------------- */
  function openResetModal() {
    el.resetModalOverlay.hidden = false;
    el.resetConfirmBtn.focus();
    document.addEventListener('keydown', onModalKeydown);
  }

  function closeResetModal() {
    el.resetModalOverlay.hidden = true;
    el.resetBtn.focus();
    document.removeEventListener('keydown', onModalKeydown);
  }

  function onModalKeydown(event) {
    if (event.key === 'Escape') closeResetModal();
  }

  function performReset() {
    localStorage.removeItem(STORAGE_KEYS.tasks);
    localStorage.removeItem(STORAGE_KEYS.notes);
    localStorage.removeItem(STORAGE_KEYS.notesTimestamp);
    localStorage.removeItem(STORAGE_KEYS.openCategories);
    // Theme preference is intentionally kept.

    taskState = {};
    openCategories = {};
    hasCelebrated = false;

    renderChecklist();
    el.notesTextarea.value = '';
    updateCharCount();
    el.notesTimestamp.textContent = 'Noch nicht gespeichert';

    closeResetModal();
    showToast('Alle Daten wurden zurückgesetzt');
  }

  /* ---------------------------------------------------------
     11. PDF EXPORT
     --------------------------------------------------------- */
  function exportToPdf() {
    if (!window.jspdf) {
      showToast('PDF-Bibliothek konnte nicht geladen werden');
      return;
    }

    const { jsPDF } = window.jspdf;
    const doc = new jsPDF({ unit: 'mm', format: 'a4' });
    const marginX = 18;
    let y = 20;

    const completed = getCompletedCount();
    const percent = TOTAL_TASKS === 0 ? 0 : Math.round((completed / TOTAL_TASKS) * 100);
    const dateStr = new Date().toLocaleDateString('de-DE');

    doc.setFont('helvetica', 'bold');
    doc.setFontSize(20);
    doc.text('Steuer Checkliste', marginX, y);
    y += 8;

    doc.setFont('helvetica', 'normal');
    doc.setFontSize(10);
    doc.setTextColor(100);
    doc.text('Exportiert am ' + dateStr, marginX, y);
    y += 10;

    doc.setDrawColor(220);
    doc.line(marginX, y, 210 - marginX, y);
    y += 8;

    doc.setTextColor(20);
    doc.setFont('helvetica', 'bold');
    doc.setFontSize(12);
    doc.text('Fortschritt: ' + percent + '% (' + completed + ' von ' + TOTAL_TASKS + ' erledigt)', marginX, y);
    y += 10;

    CHECKLIST_DATA.forEach((category) => {
      if (y > 270) { doc.addPage(); y = 20; }

      doc.setFont('helvetica', 'bold');
      doc.setFontSize(12);
      doc.setTextColor(20);
      doc.text(category.title, marginX, y);
      y += 6;

      doc.setFont('helvetica', 'normal');
      doc.setFontSize(10);

      category.tasks.forEach((taskText, idx) => {
        if (y > 280) { doc.addPage(); y = 20; }
        const checked = !!taskState[taskKey(category.id, idx)];
        const marker = checked ? '[x]' : '[ ]';
        doc.setTextColor(checked ? 120 : 20);
        const lines = doc.splitTextToSize(marker + '  ' + taskText, 170);
        doc.text(lines, marginX + 2, y);
        y += 5.5 * lines.length;
      });

      y += 4;
    });

    const notes = el.notesTextarea.value.trim();
    if (notes) {
      if (y > 250) { doc.addPage(); y = 20; }
      doc.setFont('helvetica', 'bold');
      doc.setFontSize(12);
      doc.setTextColor(20);
      doc.text('Notizen', marginX, y);
      y += 6;
      doc.setFont('helvetica', 'normal');
      doc.setFontSize(10);
      const noteLines = doc.splitTextToSize(notes, 170);
      doc.text(noteLines, marginX, y);
    }

    doc.save('steuer-checkliste.pdf');
    showToast('PDF wurde exportiert');
  }

  /* ---------------------------------------------------------
     12. TOAST NOTIFICATIONS
     --------------------------------------------------------- */
  function showToast(message) {
    clearTimeout(toastTimer);
    el.toastMessage.textContent = message;
    el.toast.hidden = false;
    refreshIcons();
    toastTimer = setTimeout(() => {
      el.toast.hidden = true;
    }, 2600);
  }

  /* ---------------------------------------------------------
     13. CONFETTI (100% completion celebration)
     --------------------------------------------------------- */
  function launchConfetti() {
    const canvas = el.confettiCanvas;
    const ctx = canvas.getContext('2d');
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    const colors = ['#004B87', '#EAB308', '#22C55E', '#111111'];
    const pieces = Array.from({ length: 140 }, () => ({
      x: Math.random() * canvas.width,
      y: -20 - Math.random() * canvas.height * 0.5,
      size: 5 + Math.random() * 6,
      color: colors[Math.floor(Math.random() * colors.length)],
      speedY: 2 + Math.random() * 3,
      speedX: -1.5 + Math.random() * 3,
      rotation: Math.random() * 360,
      rotationSpeed: -6 + Math.random() * 12
    }));

    let frame = 0;
    const maxFrames = 160;

    function draw() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      pieces.forEach((p) => {
        p.x += p.speedX;
        p.y += p.speedY;
        p.rotation += p.rotationSpeed;

        ctx.save();
        ctx.translate(p.x, p.y);
        ctx.rotate((p.rotation * Math.PI) / 180);
        ctx.fillStyle = p.color;
        ctx.fillRect(-p.size / 2, -p.size / 2, p.size, p.size * 0.6);
        ctx.restore();
      });

      frame++;
      if (frame < maxFrames) {
        requestAnimationFrame(draw);
      } else {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
      }
    }

    requestAnimationFrame(draw);
  }

  /* ---------------------------------------------------------
     14. BUTTON RIPPLE EFFECT
     --------------------------------------------------------- */
  function attachRippleEffect() {
    document.querySelectorAll('.btn').forEach((btn) => {
      btn.addEventListener('click', function (event) {
        const rect = btn.getBoundingClientRect();
        const ripple = document.createElement('span');
        const size = Math.max(rect.width, rect.height);
        ripple.className = 'ripple';
        ripple.style.width = ripple.style.height = size + 'px';
        ripple.style.left = (event.clientX - rect.left - size / 2) + 'px';
        ripple.style.top = (event.clientY - rect.top - size / 2) + 'px';
        btn.appendChild(ripple);
        setTimeout(() => ripple.remove(), 600);
      });
    });
  }

  /* ---------------------------------------------------------
     15. STICKY PROGRESS CARD (desktop only, on scroll)
     --------------------------------------------------------- */
  function initStickyProgress() {
    if (window.innerWidth < 860) return;
    let lastState = false;
    window.addEventListener('scroll', () => {
      const shouldStick = window.scrollY > 260;
      if (shouldStick !== lastState) {
        el.progressCard.classList.toggle('is-sticky-active', shouldStick);
        lastState = shouldStick;
      }
    }, { passive: true });
  }

  /* ---------------------------------------------------------
     16. KEYBOARD SHORTCUTS
     --------------------------------------------------------- */
  function initKeyboardShortcuts() {
    document.addEventListener('keydown', (event) => {
      const isModifier = event.ctrlKey || event.metaKey;
      if (!isModifier) return;

      if (event.key.toLowerCase() === 'p') {
        event.preventDefault();
        window.print();
      } else if (event.key.toLowerCase() === 'e') {
        event.preventDefault();
        exportToPdf();
      }
    });
  }

  /* ---------------------------------------------------------
     17. ICON REFRESH HELPER (Lucide re-render after DOM changes)
     --------------------------------------------------------- */
  function refreshIcons() {
    if (window.lucide && typeof window.lucide.createIcons === 'function') {
      window.lucide.createIcons();
    }
  }

  /* ---------------------------------------------------------
     18. EVENT WIRING
     --------------------------------------------------------- */
  function initEventListeners() {
    el.darkModeToggle.addEventListener('click', toggleTheme);

    el.searchToggle.addEventListener('click', toggleSearchBar);
    el.searchInput.addEventListener('input', (e) => {
      el.searchClear.hidden = e.target.value === '';
      applySearchFilter(e.target.value);
    });
    el.searchClear.addEventListener('click', clearSearch);

    el.expandAllBtn.addEventListener('click', toggleExpandAll);
    el.exportPdfBtn.addEventListener('click', exportToPdf);

    el.resetBtn.addEventListener('click', openResetModal);
    el.resetCancelBtn.addEventListener('click', closeResetModal);
    el.resetConfirmBtn.addEventListener('click', performReset);
    el.resetModalOverlay.addEventListener('click', (e) => {
      if (e.target === el.resetModalOverlay) closeResetModal();
    });

    el.ctaStart.addEventListener('click', () => {
      document.getElementById('progressCard').scrollIntoView({ behavior: 'smooth', block: 'start' });
    });

    window.addEventListener('resize', () => {
      const canvas = el.confettiCanvas;
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    });
  }

  /* ---------------------------------------------------------
     19. INIT
     --------------------------------------------------------- */
  function init() {
    initTheme();
    renderChecklist();
    initNotes();
    initEventListeners();
    attachRippleEffect();
    initStickyProgress();
    initKeyboardShortcuts();
    refreshIcons();
    if (el.footerYear) {
      el.footerYear.textContent = String(new Date().getFullYear());
    }
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', init);
  } else {
    init();
  }
})();

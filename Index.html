import React, { useState, useEffect, useCallback, useMemo } from "react";
import {
  ResponsiveContainer,
  BarChart,
  Bar,
  XAxis,
  YAxis,
  CartesianGrid,
  Tooltip,
} from "recharts";

/* ============================================================
   DATA / CONSTANTS
   ============================================================ */

const TYPES = [
  {
    id: "nicotine",
    icon: "🚬",
    glow: "#39FF88",
    title: { ru: "Никотин", en: "Nicotine" },
    sub: { ru: "сигареты, вейпы", en: "cigarettes, vapes" },
  },
  {
    id: "sugar",
    icon: "🍩",
    glow: "#FFC145",
    title: { ru: "Сахар и фастфуд", en: "Sugar & fast food" },
    sub: { ru: "сладкое, быстрые углеводы", en: "sweets, refined carbs" },
  },
  {
    id: "doomscroll",
    icon: "📱",
    glow: "#4DE3FF",
    title: { ru: "Думскроллинг", en: "Doomscrolling" },
    sub: { ru: "бесконечная лента, соцсети", en: "endless feeds, social media" },
  },
  {
    id: "alcohol",
    icon: "🍷",
    glow: "#FF6E9C",
    title: { ru: "Алкоголь", en: "Alcohol" },
    sub: { ru: "любые спиртные напитки", en: "any alcoholic drinks" },
  },
];

const TYPE_MAP = Object.fromEntries(TYPES.map((t) => [t.id, t]));
const typeLabel = (type, lang) => ({ title: type.title[lang], sub: type.sub[lang] });

const TAG_DEFS = [
  { id: "physical", ru: "Тянет физически", en: "Physical craving" },
  { id: "stress", ru: "Стресс/Нервы", en: "Stress/anxiety" },
  { id: "boredom", ru: "Скука", en: "Boredom" },
  { id: "social", ru: "За компанию", en: "Social pressure" },
  { id: "fine", ru: "Всё отлично", en: "All good" },
];
// legacy entries created before tags were stored as ids kept the raw Russian text
const LEGACY_STRESS_LABEL = "Стресс/Нервы";
function tagLabel(tagId, lang) {
  if (!tagId) return "";
  const def = TAG_DEFS.find((t) => t.id === tagId);
  return def ? def[lang] : tagId; // fall back to raw legacy text
}
function isStressTag(tagId) {
  return tagId === "stress" || tagId === LEGACY_STRESS_LABEL;
}

const HOUR = 3600 * 1000;
const DAY = 24 * HOUR;

const STORAGE_KEY = "qt_trackers_v2";
const ALCOHOL_THRESH_KEY = "qt_alcohol_thresholds_v1";
const LANG_KEY = "qt_lang_v1";
const DEFAULT_ALCOHOL_THRESHOLDS = { stage1Hours: 24, stage2Days: 14 };

/* ============================================================
   UI STRINGS
   ============================================================ */

const STRINGS = {
  ru: {
    appTitle: "Осознанный трекер отказа",
    appSub:
      "Точный таймер, честная статистика срывов и разбор состояния в реальном времени — всё хранится только на этом устройстве. Можно вести сразу несколько трекеров одновременно.",
    onboardQuestion: "С чего начнём?",
    myTrackers: "Мои трекеры",
    exportAll: "Экспорт всех",
    resetAll: "Сбросить всё",
    gearAria: "Настроить пороги",
    deleteAria: "Удалить трекер",
    confirmDeleteQ: "Удалить?",
    yes: "Да",
    no: "Нет",
    clockCaption: "дни : часы : минуты : секунды",
    relapses: "Срывов:",
    stayBtn: "Удержался 👍",
    relapseBtn: "Сорвался 💥",
    formTitleSuccess: "Что помогло удержаться?",
    formTitleFail: "Что стало триггером?",
    commentPlaceholder: "Напиши пару слов (необязательно)",
    skip: "Пропустить",
    save: "Сохранить",
    aiNormalLabel: "AI-анализ состояния",
    aiWarningLabel: "AI-предупреждение",
    chartTitle: "Прогресс за 14 дней",
    history: (n) => `История (последние ${n})`,
    exportBtn: "Экспорт",
    emptyLog: "Пока нет записей — первое действие появится здесь.",
    addTrackerTile: "+ Добавить трекер",
    addPanelTitle: "Какую ещё зависимость отслеживаем?",
    cancel: "Отмена",
    allAdded: "Все типы зависимостей уже отслеживаются.",
    settingsTitle: "Свои пороги для алкоголя",
    settingsText: "Задайте, через сколько часов/дней AI-анализ переходит к следующей стадии.",
    stage1Label: "Конец 1-й стадии, часов",
    stage2Label: "Конец 2-й стадии, дней",
    resetAllTitle: "Сбросить все трекеры?",
    resetAllText:
      "Все таймеры, счётчики срывов и история по каждому трекеру будут удалены без возможности восстановления.",
    csvHeaderSingle: "Дата,Время,Действие,Тег,Комментарий",
    csvHeaderAll: "Трекер,Дата,Время,Действие,Тег,Комментарий",
    csvSuccess: "Удержался",
    csvFail: "Сорвался",
    exportAllPrefix: "все-трекеры",
    langSwitchTo: "EN",
  },
  en: {
    appTitle: "Mindful Quit Tracker",
    appSub:
      "A precise timer, honest relapse stats, and a real-time state readout — everything stays on this device. Track several habits at once.",
    onboardQuestion: "Where should we start?",
    myTrackers: "My trackers",
    exportAll: "Export all",
    resetAll: "Reset all",
    gearAria: "Configure thresholds",
    deleteAria: "Delete tracker",
    confirmDeleteQ: "Delete?",
    yes: "Yes",
    no: "No",
    clockCaption: "days : hours : minutes : seconds",
    relapses: "Relapses:",
    stayBtn: "Stayed strong 👍",
    relapseBtn: "Relapsed 💥",
    formTitleSuccess: "What helped you stay strong?",
    formTitleFail: "What triggered it?",
    commentPlaceholder: "Add a few words (optional)",
    skip: "Skip",
    save: "Save",
    aiNormalLabel: "AI status analysis",
    aiWarningLabel: "AI warning",
    chartTitle: "14-day progress",
    history: (n) => `History (last ${n})`,
    exportBtn: "Export",
    emptyLog: "No entries yet — your first action will show up here.",
    addTrackerTile: "+ Add tracker",
    addPanelTitle: "Which other habit should we track?",
    cancel: "Cancel",
    allAdded: "All habit types are already being tracked.",
    settingsTitle: "Custom alcohol thresholds",
    settingsText: "Set how many hours/days before the AI analysis moves to the next stage.",
    stage1Label: "End of stage 1, hours",
    stage2Label: "End of stage 2, days",
    resetAllTitle: "Reset all trackers?",
    resetAllText:
      "All timers, relapse counts, and history for every tracker will be permanently deleted.",
    csvHeaderSingle: "Date,Time,Action,Tag,Comment",
    csvHeaderAll: "Tracker,Date,Time,Action,Tag,Comment",
    csvSuccess: "Stayed strong",
    csvFail: "Relapsed",
    exportAllPrefix: "all-trackers",
    langSwitchTo: "RU",
  },
};

/* ============================================================
   TIME HELPERS
   ============================================================ */

function pad(n) {
  return String(n).padStart(2, "0");
}

function splitDuration(ms) {
  const total = Math.max(0, Math.floor(ms / 1000));
  const days = Math.floor(total / 86400);
  const hours = Math.floor((total % 86400) / 3600);
  const mins = Math.floor((total % 3600) / 60);
  const secs = total % 60;
  return { days, hours, mins, secs };
}

function pluralRu(n, one, few, many) {
  const mod10 = n % 10;
  const mod100 = n % 100;
  if (mod10 === 1 && mod100 !== 11) return one;
  if ([2, 3, 4].includes(mod10) && ![12, 13, 14].includes(mod100)) return few;
  return many;
}

function formatRemaining(ms, lang) {
  if (ms <= 0) return lang === "ru" ? "меньше минуты" : "less than a minute";
  const d = Math.floor(ms / DAY);
  const h = Math.floor((ms % DAY) / HOUR);
  const m = Math.floor((ms % HOUR) / 60000);
  const parts = [];
  if (lang === "ru") {
    if (d > 0) parts.push(`${d} ${pluralRu(d, "день", "дня", "дней")}`);
    if (h > 0 && d < 3) parts.push(`${h} ${pluralRu(h, "час", "часа", "часов")}`);
    if (d === 0 && h === 0) parts.push(`${Math.max(1, m)} ${pluralRu(m, "минуту", "минуты", "минут")}`);
    return parts.join(" ") || "меньше минуты";
  }
  if (d > 0) parts.push(`${d} ${d === 1 ? "day" : "days"}`);
  if (h > 0 && d < 3) parts.push(`${h} ${h === 1 ? "hour" : "hours"}`);
  if (d === 0 && h === 0) parts.push(`${Math.max(1, m)} ${m === 1 ? "minute" : "minutes"}`);
  return parts.join(" ") || "less than a minute";
}

function formatClock(elapsed) {
  const { days, hours, mins, secs } = splitDuration(elapsed);
  return `${pad(days)} : ${pad(hours)} : ${pad(mins)} : ${pad(secs)}`;
}

function formatLogTime(ts) {
  const d = new Date(ts);
  return `${pad(d.getDate())}.${pad(d.getMonth() + 1)} ${pad(d.getHours())}:${pad(d.getMinutes())}`;
}

function generateId() {
  return `${Date.now()}-${Math.random().toString(36).slice(2, 8)}`;
}

/* ============================================================
   AI ANALYSIS ENGINE
   ============================================================ */

function analyze(typeId, elapsed, log, alcoholThresholds, lang) {
  const fails = log.filter((e) => e.action === "fail");
  const lastThree = fails.slice(0, 3);
  const stressCount = lastThree.filter((e) => isStressTag(e.tag)).length;
  if (lastThree.length >= 3 && stressCount > 2) {
    return lang === "ru"
      ? {
          kind: "warning",
          title: "Скрытый паттерн обнаружен",
          text: "Ваш скрытый тип зависимости — «стрессовый». Вы срываетесь, когда нервничаете, а не когда есть физический повод. Если прямо сейчас не заменить триггер на дыхательную гимнастику 4-8 (вдох на 4 счёта, задержка на 8, долгий выдох), ломка затянется на месяцы.",
        }
      : {
          kind: "warning",
          title: "Hidden pattern detected",
          text: "Your hidden trigger type is 'stress-driven' — you relapse when you're anxious, not when there's a physical urge. Unless you swap the trigger for 4-8 breathing (inhale for 4 counts, hold for 8, exhale slowly) right now, the withdrawal will stretch into months.",
        };
  }

  const R = (ms) => formatRemaining(ms, lang);
  const days = splitDuration(elapsed).days;

  if (typeId === "nicotine") {
    if (elapsed < 3 * HOUR) {
      return lang === "ru"
        ? { kind: "stage", title: "Пиковая фаза", text: `Идёт жёсткая физическая ломка — организм выводит первый никотин. Потерпите ещё ${R(3 * HOUR - elapsed)}. Это самый пик, дальше будет легче.` }
        : { kind: "stage", title: "Peak phase", text: `You're in the hardest part of withdrawal — your body is clearing out the first nicotine. Hang on about ${R(3 * HOUR - elapsed)} more. This is the peak, it gets easier from here.` };
    }
    if (elapsed < 3 * DAY) {
      return lang === "ru"
        ? { kind: "stage", title: "Очищение", text: `Идёт очищение лёгких. Физическая тяга угаснет примерно через ${R(3 * DAY - elapsed)}. Держитесь.` }
        : { kind: "stage", title: "Clearing out", text: `Your lungs are clearing out. The physical craving should fade in about ${R(3 * DAY - elapsed)}. Stay strong.` };
    }
    if (elapsed < 60 * DAY) {
      return lang === "ru"
        ? { kind: "stage", title: "Стабилизация", text: `Острая фаза позади. Организм адаптируется без никотина — до полного затухания рецепторов ещё ${R(60 * DAY - elapsed)}. Основная работа теперь психологическая.` }
        : { kind: "stage", title: "Stabilizing", text: `The acute phase is over. Your body is adapting without nicotine — full receptor reset in about ${R(60 * DAY - elapsed)}. The main work now is psychological.` };
    }
    return lang === "ru"
      ? { kind: "stage", title: "Свобода", text: `Уже ${days} дней без никотина. Физической зависимости больше нет — вы бросили примерно на 95%. Осталось следить только за редкими психологическими триггерами.` }
      : { kind: "stage", title: "Free", text: `It's been ${days} days without nicotine. The physical addiction is gone — you've beaten roughly 95% of it. Now just watch for occasional psychological triggers.` };
  }

  if (typeId === "sugar") {
    if (elapsed < DAY) {
      return lang === "ru"
        ? { kind: "stage", title: "Дофаминовая яма", text: `Уровень глюкозы упал, мозг требует привычного дофамина. Сильнейшая тяга к сладкому продлится ещё около ${R(DAY - elapsed)}. Пейте воду.` }
        : { kind: "stage", title: "Dopamine dip", text: `Blood sugar dropped and your brain wants its usual dopamine hit. The strongest craving will last about ${R(DAY - elapsed)} more. Drink some water.` };
    }
    if (elapsed < 7 * DAY) {
      return lang === "ru"
        ? { kind: "stage", title: "Перестройка", text: `Идёт перестройка рецепторов и нормализация инсулина. Возможны перепады настроения — этот кризис отступит через ${R(7 * DAY - elapsed)}.` }
        : { kind: "stage", title: "Rewiring", text: `Your receptors are rewiring and insulin is normalizing. Mood swings are possible — this will pass in about ${R(7 * DAY - elapsed)}.` };
    }
    if (elapsed < 30 * DAY) {
      return lang === "ru"
        ? { kind: "stage", title: "Новый баланс", text: `Инсулиновые качели позади. Вкусовые рецепторы заново учатся ценить несладкую еду — полная перестройка завершится через ${R(30 * DAY - elapsed)}.` }
        : { kind: "stage", title: "New balance", text: `The insulin rollercoaster is behind you. Your taste buds are relearning to enjoy unsweetened food — the full reset finishes in about ${R(30 * DAY - elapsed)}.` };
    }
    return lang === "ru"
      ? { kind: "stage", title: "Метаболизм перестроен", text: `Уже месяц без сахарных качелей! Метаболизм перестроился, вы победили основную тягу.` }
      : { kind: "stage", title: "Metabolism reset", text: `A month without the sugar rollercoaster! Your metabolism has reset and you've beaten the main craving.` };
  }

  if (typeId === "doomscroll") {
    if (elapsed < 6 * HOUR) {
      return lang === "ru"
        ? { kind: "stage", title: "Дофаминовый голод", text: `Мозг паникует без дешёвого дофамина из ленты. Самый жёсткий зуд проверить телефон пройдёт через ${R(6 * HOUR - elapsed)}. Уберите смартфон в другую комнату.` }
        : { kind: "stage", title: "Dopamine hunger", text: `Your brain is panicking without its cheap feed dopamine. The sharpest urge to check your phone will fade in about ${R(6 * HOUR - elapsed)}. Put your phone in another room.` };
    }
    if (elapsed < 4 * DAY) {
      return lang === "ru"
        ? { kind: "stage", title: "Новый фокус", text: `Формируется новая привычка фокусироваться. Тяга зайти в соцсети ослабнет через ${R(4 * DAY - elapsed)}.` }
        : { kind: "stage", title: "New focus", text: `A new habit of focusing is forming. The urge to open social apps will ease in about ${R(4 * DAY - elapsed)}.` };
    }
    return lang === "ru"
      ? { kind: "stage", title: "Внимание возвращается", text: `Автоматический рефлекс тянуться к телефону практически угас. Продолжайте замечать моменты, когда рука сама тянется за ним — это последний рубеж привычки.` }
      : { kind: "stage", title: "Attention returning", text: `The automatic reflex to reach for your phone has mostly faded. Keep noticing the moments your hand reaches for it anyway — that's the last stretch of the habit.` };
  }

  // alcohol — thresholds are user-configurable, fall back to defaults
  const th = alcoholThresholds || DEFAULT_ALCOHOL_THRESHOLDS;
  const stage1End = th.stage1Hours * HOUR;
  const stage2End = th.stage2Days * DAY;
  if (elapsed < stage1End) {
    return lang === "ru"
      ? { kind: "stage", title: "Первые сутки", text: `Нервная система всё ещё возбуждена без привычного седативного эффекта. Возможны раздражительность и плохой сон ещё около ${R(stage1End - elapsed)}. Если ощущения сильные — дрожь, сильная тревога, — лучше обсудить это с врачом.` }
      : { kind: "stage", title: "First day", text: `Your nervous system is still wound up without its usual sedative effect. Irritability and poor sleep are possible for about ${R(stage1End - elapsed)} more. If symptoms are strong — shaking, intense anxiety — it's best to talk to a doctor.` };
  }
  if (elapsed < stage2End) {
    return lang === "ru"
      ? { kind: "stage", title: "Восстановление сна", text: `Печень и сон постепенно восстанавливаются. Эмоциональные качели ещё возможны — стабилизация ожидается через ${R(stage2End - elapsed)}.` }
      : { kind: "stage", title: "Sleep recovering", text: `Your liver and sleep are gradually recovering. Emotional swings are still possible — things should stabilize in about ${R(stage2End - elapsed)}.` };
  }
  return lang === "ru"
    ? { kind: "stage", title: "Новая база", text: `Уже ${days} дней. Сон и энергия заметно ровнее — теперь дело за психологическими привычками и триггерами.` }
    : { kind: "stage", title: "New baseline", text: `It's been ${days} days. Sleep and energy are noticeably steadier — now it's about the psychological habits and triggers.` };
}

/* ============================================================
   PERSISTENCE
   ============================================================ */

function loadTrackers() {
  try {
    const raw = localStorage.getItem(STORAGE_KEY);
    if (raw) {
      const parsed = JSON.parse(raw);
      if (Array.isArray(parsed.trackers)) return parsed.trackers;
    }
    const oldRaw = localStorage.getItem("qt_state_v1");
    if (oldRaw) {
      const old = JSON.parse(oldRaw);
      if (old && old.typeId && old.startTime) {
        return [
          {
            id: generateId(),
            typeId: old.typeId,
            startTime: old.startTime,
            failCount: old.failCount || 0,
            log: old.log || [],
          },
        ];
      }
    }
    return [];
  } catch {
    return [];
  }
}

function saveTrackers(trackers) {
  try {
    localStorage.setItem(STORAGE_KEY, JSON.stringify({ trackers }));
  } catch {
    /* storage unavailable — fail silently */
  }
}

function loadAlcoholThresholds() {
  try {
    const raw = localStorage.getItem(ALCOHOL_THRESH_KEY);
    if (!raw) return DEFAULT_ALCOHOL_THRESHOLDS;
    const parsed = JSON.parse(raw);
    return {
      stage1Hours: Number(parsed.stage1Hours) || DEFAULT_ALCOHOL_THRESHOLDS.stage1Hours,
      stage2Days: Number(parsed.stage2Days) || DEFAULT_ALCOHOL_THRESHOLDS.stage2Days,
    };
  } catch {
    return DEFAULT_ALCOHOL_THRESHOLDS;
  }
}

function saveAlcoholThresholds(th) {
  try {
    localStorage.setItem(ALCOHOL_THRESH_KEY, JSON.stringify(th));
  } catch {
    /* storage unavailable — fail silently */
  }
}

function loadLang() {
  try {
    const raw = localStorage.getItem(LANG_KEY);
    if (raw === "ru" || raw === "en") return raw;
  } catch {
    /* ignore */
  }
  if (typeof navigator !== "undefined" && /^ru/i.test(navigator.language || "")) return "ru";
  return "en";
}

function saveLang(lang) {
  try {
    localStorage.setItem(LANG_KEY, lang);
  } catch {
    /* storage unavailable — fail silently */
  }
}

/* ---------- sound + vibration feedback ---------- */

let sharedAudioCtx = null;
function getAudioCtx() {
  if (typeof window === "undefined") return null;
  const Ctor = window.AudioContext || window.webkitAudioContext;
  if (!Ctor) return null;
  if (!sharedAudioCtx) sharedAudioCtx = new Ctor();
  if (sharedAudioCtx.state === "suspended") sharedAudioCtx.resume();
  return sharedAudioCtx;
}

function playTone(kind) {
  const ctx = getAudioCtx();
  if (!ctx) return;
  const now = ctx.currentTime;

  if (kind === "fail") {
    const osc = ctx.createOscillator();
    const gain = ctx.createGain();
    osc.type = "sawtooth";
    osc.frequency.setValueAtTime(320, now);
    osc.frequency.exponentialRampToValueAtTime(90, now + 0.35);
    gain.gain.setValueAtTime(0.09, now);
    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.38);
    osc.connect(gain).connect(ctx.destination);
    osc.start(now);
    osc.stop(now + 0.4);
  } else {
    const osc = ctx.createOscillator();
    const gain = ctx.createGain();
    osc.type = "sine";
    osc.frequency.setValueAtTime(520, now);
    osc.frequency.exponentialRampToValueAtTime(880, now + 0.18);
    gain.gain.setValueAtTime(0.07, now);
    gain.gain.exponentialRampToValueAtTime(0.001, now + 0.3);
    osc.connect(gain).connect(ctx.destination);
    osc.start(now);
    osc.stop(now + 0.32);
  }
}

function vibrateDevice(kind) {
  if (typeof navigator === "undefined" || !navigator.vibrate) return;
  navigator.vibrate(kind === "fail" ? [90, 50, 90] : [30]);
}

/* ---------- export ---------- */

function exportLogToCSV(log, typeTitle, lang) {
  const S = STRINGS[lang];
  const rows = log.map((e) => {
    const d = new Date(e.ts);
    const date = `${pad(d.getDate())}.${pad(d.getMonth() + 1)}.${d.getFullYear()}`;
    const time = `${pad(d.getHours())}:${pad(d.getMinutes())}`;
    const action = e.action === "success" ? S.csvSuccess : S.csvFail;
    const tag = tagLabel(e.tag, lang);
    const comment = (e.comment || "").replace(/"/g, "'").replace(/\n/g, " ");
    return [date, time, action, tag, `"${comment}"`].join(",");
  });
  const csv = [S.csvHeaderSingle, ...rows].join("\n");
  const blob = new Blob(["\uFEFF" + csv], { type: "text/csv;charset=utf-8;" });
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  const stamp = new Date().toISOString().slice(0, 10);
  a.href = url;
  a.download = `${typeTitle || "history"}-${stamp}.csv`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}

function exportAllToCSV(trackers, lang) {
  const S = STRINGS[lang];
  const rows = [];
  trackers.forEach((t) => {
    const title = TYPE_MAP[t.typeId] ? typeLabel(TYPE_MAP[t.typeId], lang).title : t.typeId;
    t.log.forEach((e) => {
      const d = new Date(e.ts);
      const date = `${pad(d.getDate())}.${pad(d.getMonth() + 1)}.${d.getFullYear()}`;
      const time = `${pad(d.getHours())}:${pad(d.getMinutes())}`;
      const action = e.action === "success" ? S.csvSuccess : S.csvFail;
      const tag = tagLabel(e.tag, lang);
      const comment = (e.comment || "").replace(/"/g, "'").replace(/\n/g, " ");
      rows.push([title, date, time, action, tag, `"${comment}"`].join(","));
    });
  });
  const csv = [S.csvHeaderAll, ...rows].join("\n");
  const blob = new Blob(["\uFEFF" + csv], { type: "text/csv;charset=utf-8;" });
  const url = URL.createObjectURL(blob);
  const a = document.createElement("a");
  const stamp = new Date().toISOString().slice(0, 10);
  a.href = url;
  a.download = `${S.exportAllPrefix}-${stamp}.csv`;
  document.body.appendChild(a);
  a.click();
  document.body.removeChild(a);
  URL.revokeObjectURL(url);
}

/* ---------- chart aggregation ---------- */

function dayKey(ts) {
  const d = new Date(ts);
  return `${d.getFullYear()}-${pad(d.getMonth() + 1)}-${pad(d.getDate())}`;
}

function buildDailyStats(log, days = 14) {
  const buckets = new Map();
  const today = new Date();
  for (let i = days - 1; i >= 0; i--) {
    const d = new Date(today);
    d.setDate(d.getDate() - i);
    const key = dayKey(d.getTime());
    buckets.set(key, {
      key,
      label: `${pad(d.getDate())}.${pad(d.getMonth() + 1)}`,
      success: 0,
      fail: 0,
    });
  }
  log.forEach((e) => {
    const key = dayKey(e.ts);
    const bucket = buckets.get(key);
    if (!bucket) return;
    if (e.action === "success") bucket.success += 1;
    else bucket.fail += 1;
  });
  return Array.from(buckets.values());
}

/* ============================================================
   UI PIECES
   ============================================================ */

function TagChip({ label, active, onClick, tone }) {
  return (
    <button
      type="button"
      onClick={onClick}
      className="qt-chip"
      style={{
        borderColor: active ? tone : "rgba(255,255,255,0.14)",
        color: active ? tone : "#9AA5B8",
        background: active ? `${tone}14` : "transparent",
      }}
    >
      {label}
    </button>
  );
}

function LogRow({ entry, lang }) {
  const isSuccess = entry.action === "success";
  const label = tagLabel(entry.tag, lang);
  return (
    <div className="qt-log-row">
      <span className="qt-log-icon" style={{ color: isSuccess ? "#39FF88" : "#FF4D5E" }}>
        {isSuccess ? "👍" : "💥"}
      </span>
      <div className="qt-log-body">
        <div className="qt-log-top">
          <span className="qt-log-time">{formatLogTime(entry.ts)}</span>
          {label && <span className="qt-log-tag">{label}</span>}
        </div>
        {entry.comment && <div className="qt-log-comment">{entry.comment}</div>}
      </div>
    </div>
  );
}

function ProgressChart({ log, lang }) {
  const S = STRINGS[lang];
  const data = useMemo(() => buildDailyStats(log, 14), [log]);
  const totalSuccess = log.filter((e) => e.action === "success").length;
  const totalFail = log.filter((e) => e.action === "fail").length;

  return (
    <div className="qt-chart-card">
      <div className="qt-chart-head">
        <span className="qt-chart-title">{S.chartTitle}</span>
        <div className="qt-chart-legend">
          <span className="qt-legend-dot" style={{ background: "#39FF88" }} />
          <span>{totalSuccess}</span>
          <span className="qt-legend-dot" style={{ background: "#FF4D5E", marginLeft: 10 }} />
          <span>{totalFail}</span>
        </div>
      </div>
      <div className="qt-chart-body">
        <ResponsiveContainer width="100%" height={140}>
          <BarChart data={data} barGap={2} margin={{ top: 4, right: 0, left: -24, bottom: 0 }}>
            <CartesianGrid vertical={false} stroke="rgba(255,255,255,0.06)" />
            <XAxis
              dataKey="label"
              tick={{ fill: "#5C6479", fontSize: 9 }}
              axisLine={{ stroke: "rgba(255,255,255,0.08)" }}
              tickLine={false}
              interval={1}
            />
            <YAxis
              allowDecimals={false}
              tick={{ fill: "#5C6479", fontSize: 9 }}
              axisLine={false}
              tickLine={false}
              width={24}
            />
            <Tooltip
              cursor={{ fill: "rgba(255,255,255,0.04)" }}
              contentStyle={{
                background: "#10151F",
                border: "1px solid rgba(255,255,255,0.12)",
                borderRadius: 10,
                fontSize: 12,
              }}
              labelStyle={{ color: "#C7CEDC" }}
            />
            <Bar dataKey="success" fill="#39FF88" radius={[3, 3, 0, 0]} maxBarSize={10} />
            <Bar dataKey="fail" fill="#FF4D5E" radius={[3, 3, 0, 0]} maxBarSize={10} />
          </BarChart>
        </ResponsiveContainer>
      </div>
    </div>
  );
}

/* ============================================================
   TRACKER CARD — one addiction, fully self-contained
   ============================================================ */

function TrackerCard({ tracker, now, alcoholThresholds, lang, onFail, onSuccess, onSubmit, onSkip, onDelete, onOpenSettings }) {
  const S = STRINGS[lang];
  const [openForm, setOpenForm] = useState(null);
  const [selectedTag, setSelectedTag] = useState(null);
  const [comment, setComment] = useState("");
  const [logExpanded, setLogExpanded] = useState(false);
  const [confirmDelete, setConfirmDelete] = useState(false);

  const type = TYPE_MAP[tracker.typeId];
  const label = typeLabel(type, lang);
  const elapsed = Math.max(0, now - tracker.startTime);
  const ai = useMemo(
    () => analyze(tracker.typeId, elapsed, tracker.log, alcoholThresholds, lang),
    [tracker.typeId, elapsed, tracker.log, alcoholThresholds, lang]
  );

  const handleFailClick = () => {
    onFail(tracker.id);
    setOpenForm("fail");
    setSelectedTag(null);
    setComment("");
  };

  const handleSuccessClick = () => {
    onSuccess(tracker.id);
    setOpenForm("success");
    setSelectedTag(null);
    setComment("");
  };

  const submitForm = () => {
    onSubmit(tracker.id, openForm, selectedTag, comment.trim());
    setOpenForm(null);
    setSelectedTag(null);
    setComment("");
  };

  const skipForm = () => {
    onSkip(tracker.id, openForm);
    setOpenForm(null);
    setSelectedTag(null);
    setComment("");
  };

  return (
    <div className="qt-card qt-fade-in">
      <div className="qt-card-header">
        <div className="qt-header-label">
          <span className="qt-header-icon">{type.icon}</span>
          <span>{label.title}</span>
        </div>
        <div className="qt-header-actions">
          {tracker.typeId === "alcohol" && (
            <button type="button" className="qt-gear-btn" onClick={onOpenSettings} aria-label={S.gearAria}>
              ⚙
            </button>
          )}
          {!confirmDelete ? (
            <button
              type="button"
              className="qt-gear-btn qt-gear-btn-danger"
              onClick={() => setConfirmDelete(true)}
              aria-label={S.deleteAria}
            >
              ✕
            </button>
          ) : (
            <span className="qt-inline-confirm">
              {S.confirmDeleteQ}
              <button type="button" className="qt-inline-confirm-yes" onClick={() => onDelete(tracker.id)}>
                {S.yes}
              </button>
              <button type="button" className="qt-inline-confirm-no" onClick={() => setConfirmDelete(false)}>
                {S.no}
              </button>
            </span>
          )}
        </div>
      </div>

      <div className="qt-timer-wrap">
        <div className="qt-timer" style={{ textShadow: `0 0 18px ${type.glow}55, 0 0 38px ${type.glow}22` }}>
          {formatClock(elapsed).split(" ").map((ch, i) => (
            <span key={i} className={ch === ":" ? "qt-timer-colon" : "qt-timer-digit"}>
              {ch}
            </span>
          ))}
        </div>
        <div className="qt-timer-caption">{S.clockCaption}</div>
        <div className="qt-fail-pill">
          {S.relapses} <b>{tracker.failCount}</b>
        </div>
      </div>

      <div className="qt-actions">
        <button type="button" className="qt-btn qt-btn-success" onClick={handleSuccessClick}>
          {S.stayBtn}
        </button>
        <button type="button" className="qt-btn qt-btn-fail" onClick={handleFailClick}>
          {S.relapseBtn}
        </button>
      </div>

      {openForm && (
        <div className="qt-form qt-fade-in">
          <div className="qt-form-title">{openForm === "success" ? S.formTitleSuccess : S.formTitleFail}</div>
          <div className="qt-chips">
            {TAG_DEFS.map((t) => (
              <TagChip
                key={t.id}
                label={t[lang]}
                active={selectedTag === t.id}
                tone={openForm === "success" ? "#39FF88" : "#FF4D5E"}
                onClick={() => setSelectedTag((cur) => (cur === t.id ? null : t.id))}
              />
            ))}
          </div>
          <textarea
            className="qt-textarea"
            placeholder={S.commentPlaceholder}
            value={comment}
            onChange={(e) => setComment(e.target.value)}
            rows={2}
          />
          <div className="qt-form-actions">
            <button type="button" className="qt-link-btn" onClick={skipForm}>
              {S.skip}
            </button>
            <button
              type="button"
              className="qt-btn-small"
              style={{ background: openForm === "success" ? "#39FF88" : "#FF4D5E" }}
              onClick={submitForm}
            >
              {S.save}
            </button>
          </div>
        </div>
      )}

      {ai && (
        <div className={`qt-ai ${ai.kind === "warning" ? "qt-ai-warning" : ""}`}>
          <div className="qt-ai-top">
            <span className="qt-ai-dot" />
            <span className="qt-ai-label">{ai.kind === "warning" ? S.aiWarningLabel : S.aiNormalLabel}</span>
          </div>
          <div className="qt-ai-title">{ai.title}</div>
          <p className="qt-ai-text">{ai.text}</p>
        </div>
      )}

      {tracker.log.length > 0 && <ProgressChart log={tracker.log} lang={lang} />}

      <div className="qt-log-section">
        <div className="qt-log-toggle-row">
          <button type="button" className="qt-log-toggle" onClick={() => setLogExpanded((v) => !v)}>
            <span>{S.history(Math.min(5, tracker.log.length))}</span>
            <span className={`qt-chevron ${logExpanded ? "qt-chevron-open" : ""}`}>⌄</span>
          </button>
          {tracker.log.length > 0 && (
            <button
              type="button"
              className="qt-export-btn"
              onClick={() => exportLogToCSV(tracker.log, label.title, lang)}
            >
              {S.exportBtn}
            </button>
          )}
        </div>
        {logExpanded && (
          <div className="qt-log-list qt-fade-in">
            {tracker.log.length === 0 ? (
              <div className="qt-log-empty">{S.emptyLog}</div>
            ) : (
              tracker.log.slice(0, 5).map((e, i) => <LogRow key={e.ts + "-" + i} entry={e} lang={lang} />)
            )}
          </div>
        )}
      </div>
    </div>
  );
}

/* ============================================================
   ONBOARDING + ADD-TRACKER PICKER
   ============================================================ */

function TypePicker({ availableTypes, lang, onSelect }) {
  return (
    <div className="qt-type-grid">
      {availableTypes.map((t) => {
        const label = typeLabel(t, lang);
        return (
          <button
            key={t.id}
            type="button"
            className="qt-type-card"
            style={{ "--glow": t.glow }}
            onClick={() => onSelect(t.id)}
          >
            <span className="qt-type-icon">{t.icon}</span>
            <span className="qt-type-title">{label.title}</span>
            <span className="qt-type-sub">{label.sub}</span>
          </button>
        );
      })}
    </div>
  );
}

function Onboarding({ lang, onSelect }) {
  const S = STRINGS[lang];
  return (
    <div className="qt-onboard qt-fade-in">
      <div className="qt-onboard-eyebrow-icon">◈</div>
      <h1 className="qt-onboard-title">{S.appTitle}</h1>
      <p className="qt-onboard-sub">{S.appSub}</p>
      <div className="qt-onboard-question">{S.onboardQuestion}</div>
      <TypePicker availableTypes={TYPES} lang={lang} onSelect={onSelect} />
    </div>
  );
}

/* ============================================================
   MAIN APP
   ============================================================ */

export default function App() {
  const [trackers, setTrackers] = useState([]);
  const [now, setNow] = useState(Date.now());
  const [ready, setReady] = useState(false);
  const [lang, setLang] = useState("ru");

  const [alcoholThresholds, setAlcoholThresholds] = useState(DEFAULT_ALCOHOL_THRESHOLDS);
  const [showSettings, setShowSettings] = useState(false);
  const [thStage1, setThStage1] = useState(String(DEFAULT_ALCOHOL_THRESHOLDS.stage1Hours));
  const [thStage2, setThStage2] = useState(String(DEFAULT_ALCOHOL_THRESHOLDS.stage2Days));

  const [showAddPicker, setShowAddPicker] = useState(false);
  const [confirmResetAll, setConfirmResetAll] = useState(false);

  useEffect(() => {
    setTrackers(loadTrackers());
    const th = loadAlcoholThresholds();
    setAlcoholThresholds(th);
    setThStage1(String(th.stage1Hours));
    setThStage2(String(th.stage2Days));
    setLang(loadLang());
    setReady(true);
  }, []);

  useEffect(() => {
    const id = setInterval(() => setNow(Date.now()), 1000);
    return () => clearInterval(id);
  }, []);

  useEffect(() => {
    if (!ready) return;
    saveTrackers(trackers);
  }, [ready, trackers]);

  useEffect(() => {
    if (!ready) return;
    saveLang(lang);
  }, [ready, lang]);

  const S = STRINGS[lang];
  const usedTypeIds = trackers.map((t) => t.typeId);
  const availableTypes = TYPES.filter((t) => !usedTypeIds.includes(t.id));

  const addTracker = useCallback((typeId) => {
    setTrackers((list) => [
      ...list,
      { id: generateId(), typeId, startTime: Date.now(), failCount: 0, log: [] },
    ]);
    setShowAddPicker(false);
  }, []);

  const deleteTracker = useCallback((id) => {
    setTrackers((list) => list.filter((t) => t.id !== id));
  }, []);

  const handleFail = useCallback((id) => {
    playTone("fail");
    vibrateDevice("fail");
    setTrackers((list) =>
      list.map((t) => (t.id === id ? { ...t, startTime: Date.now(), failCount: t.failCount + 1 } : t))
    );
  }, []);

  const handleSuccess = useCallback(() => {
    playTone("success");
    vibrateDevice("success");
  }, []);

  const handleSubmit = useCallback((id, action, tag, comment) => {
    const entry = { ts: Date.now(), action, tag, comment };
    setTrackers((list) => list.map((t) => (t.id === id ? { ...t, log: [entry, ...t.log].slice(0, 200) } : t)));
  }, []);

  const handleSkip = useCallback((id, action) => {
    const entry = { ts: Date.now(), action, tag: null, comment: "" };
    setTrackers((list) => list.map((t) => (t.id === id ? { ...t, log: [entry, ...t.log].slice(0, 200) } : t)));
  }, []);

  const saveSettings = useCallback(() => {
    const stage1Hours = Math.max(1, Number(thStage1) || DEFAULT_ALCOHOL_THRESHOLDS.stage1Hours);
    const stage2Days = Math.max(1, Number(thStage2) || DEFAULT_ALCOHOL_THRESHOLDS.stage2Days);
    const th = { stage1Hours, stage2Days };
    setAlcoholThresholds(th);
    saveAlcoholThresholds(th);
    setShowSettings(false);
  }, [thStage1, thStage2]);

  const doResetAll = useCallback(() => {
    setTrackers([]);
    setConfirmResetAll(false);
  }, []);

  if (!ready) return null;

  return (
    <div className="qt-root">
      <style>{CSS}</style>

      <button type="button" className="qt-lang-switch" onClick={() => setLang((l) => (l === "ru" ? "en" : "ru"))}>
        {S.langSwitchTo}
      </button>

      {trackers.length === 0 ? (
        <Onboarding lang={lang} onSelect={addTracker} />
      ) : (
        <div className="qt-shell">
          <header className="qt-page-header">
            <div className="qt-page-title">{S.myTrackers}</div>
            <div className="qt-header-actions">
              {trackers.length > 1 && (
                <button type="button" className="qt-reset-btn" onClick={() => exportAllToCSV(trackers, lang)}>
                  {S.exportAll}
                </button>
              )}
              <button type="button" className="qt-reset-btn" onClick={() => setConfirmResetAll(true)}>
                {S.resetAll}
              </button>
            </div>
          </header>

          <div className="qt-tracker-list">
            {trackers.map((t) => (
              <TrackerCard
                key={t.id}
                tracker={t}
                now={now}
                alcoholThresholds={alcoholThresholds}
                lang={lang}
                onFail={handleFail}
                onSuccess={handleSuccess}
                onSubmit={handleSubmit}
                onSkip={handleSkip}
                onDelete={deleteTracker}
                onOpenSettings={() => setShowSettings(true)}
              />
            ))}
          </div>

          {availableTypes.length > 0 ? (
            !showAddPicker ? (
              <button type="button" className="qt-add-tile" onClick={() => setShowAddPicker(true)}>
                {S.addTrackerTile}
              </button>
            ) : (
              <div className="qt-add-panel qt-fade-in">
                <div className="qt-form-title">{S.addPanelTitle}</div>
                <TypePicker availableTypes={availableTypes} lang={lang} onSelect={addTracker} />
                <button type="button" className="qt-link-btn" onClick={() => setShowAddPicker(false)}>
                  {S.cancel}
                </button>
              </div>
            )
          ) : (
            <div className="qt-all-added">{S.allAdded}</div>
          )}
        </div>
      )}

      {showSettings && (
        <div className="qt-modal-backdrop" onClick={() => setShowSettings(false)}>
          <div className="qt-modal" onClick={(e) => e.stopPropagation()}>
            <div className="qt-modal-title">{S.settingsTitle}</div>
            <p className="qt-modal-text">{S.settingsText}</p>
            <label className="qt-field-label">
              {S.stage1Label}
              <input
                type="number"
                min="1"
                className="qt-input"
                value={thStage1}
                onChange={(e) => setThStage1(e.target.value)}
              />
            </label>
            <label className="qt-field-label">
              {S.stage2Label}
              <input
                type="number"
                min="1"
                className="qt-input"
                value={thStage2}
                onChange={(e) => setThStage2(e.target.value)}
              />
            </label>
            <div className="qt-modal-actions">
              <button type="button" className="qt-link-btn" onClick={() => setShowSettings(false)}>
                {S.cancel}
              </button>
              <button type="button" className="qt-btn-small" style={{ background: "#4DE3FF" }} onClick={saveSettings}>
                {S.save}
              </button>
            </div>
          </div>
        </div>
      )}

      {confirmResetAll && (
        <div className="qt-modal-backdrop" onClick={() => setConfirmResetAll(false)}>
          <div className="qt-modal" onClick={(e) => e.stopPropagation()}>
            <div className="qt-modal-title">{S.resetAllTitle}</div>
            <p className="qt-modal-text">{S.resetAllText}</p>
            <div className="qt-modal-actions">
              <button type="button" className="qt-link-btn" onClick={() => setConfirmResetAll(false)}>
                {S.cancel}
              </button>
              <button type="button" className="qt-btn-small" style={{ background: "#FF4D5E" }} onClick={doResetAll}>
                {S.resetAll}
              </button>
            </div>
          </div>
        </div>
      )}
    </div>
  );
}

/* ============================================================
   STYLES
   ============================================================ */

const CSS = `
  .qt-root {
    position: relative;
    min-height: 100%;
    width: 100%;
    background: #0B0F19;
    background-image:
      radial-gradient(circle at 20% 0%, rgba(77,227,255,0.06), transparent 45%),
      radial-gradient(circle at 85% 15%, rgba(57,255,136,0.05), transparent 40%);
    color: #E7ECF5;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Inter, Roboto, sans-serif;
    padding: 28px 18px 48px;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
  }
  .qt-root * { box-sizing: border-box; }

  .qt-lang-switch {
    position: absolute; top: 16px; right: 16px;
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(255,255,255,0.14);
    color: #9AA5B8;
    font-size: 11px; font-weight: 600; letter-spacing: 0.03em;
    padding: 5px 11px;
    border-radius: 999px;
    cursor: pointer;
    z-index: 20;
  }
  .qt-lang-switch:hover { border-color: rgba(77,227,255,0.4); color: #4DE3FF; }

  .qt-shell { width: 100%; max-width: 460px; }

  .qt-fade-in { animation: qtFadeUp .5s ease both; }
  @keyframes qtFadeUp {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .qt-page-header {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 18px; padding-right: 46px;
  }
  .qt-page-title { font-size: 17px; font-weight: 600; }

  .qt-onboard { width: 100%; max-width: 440px; text-align: center; padding-top: 24px; margin: 0 auto; }
  .qt-onboard-eyebrow-icon {
    font-size: 22px; color: #4DE3FF; margin-bottom: 14px;
    text-shadow: 0 0 16px rgba(77,227,255,0.6);
  }
  .qt-onboard-title {
    font-size: 26px; font-weight: 600; letter-spacing: -0.01em;
    margin: 0 0 10px; line-height: 1.25;
  }
  .qt-onboard-sub {
    color: #8A93A6; font-size: 14.5px; line-height: 1.55;
    margin: 0 0 30px; padding: 0 6px;
  }
  .qt-onboard-question {
    font-size: 15px; color: #C7CEDC; margin-bottom: 16px; font-weight: 500;
  }
  .qt-type-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }
  .qt-type-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 16px;
    padding: 20px 12px;
    display: flex; flex-direction: column; align-items: center; gap: 6px;
    color: #E7ECF5;
    cursor: pointer;
    transition: border-color .2s ease, transform .15s ease, box-shadow .2s ease;
  }
  .qt-type-card:hover, .qt-type-card:focus-visible {
    border-color: var(--glow);
    box-shadow: 0 0 0 1px var(--glow) inset, 0 0 24px -8px var(--glow);
    transform: translateY(-2px);
    outline: none;
  }
  .qt-type-icon { font-size: 26px; }
  .qt-type-title { font-size: 14px; font-weight: 600; margin-top: 2px; }
  .qt-type-sub { font-size: 11.5px; color: #7C8598; }

  .qt-tracker-list { display: flex; flex-direction: column; gap: 18px; }
  .qt-card {
    border: 1px solid rgba(255,255,255,0.07);
    border-radius: 22px;
    padding: 16px 16px 18px;
    background: rgba(255,255,255,0.012);
  }

  .qt-card-header {
    display: flex; align-items: center; justify-content: space-between;
    margin-bottom: 16px;
  }
  .qt-header-label {
    display: flex; align-items: center; gap: 8px;
    font-size: 14px; color: #A9B2C3; font-weight: 500;
  }
  .qt-header-icon { font-size: 16px; }
  .qt-header-actions { display: flex; align-items: center; gap: 10px; }
  .qt-reset-btn {
    background: none; border: none; color: #5C6479;
    font-size: 11.5px; cursor: pointer; padding: 4px 0;
    text-decoration: underline; text-underline-offset: 2px;
  }
  .qt-reset-btn:hover { color: #8A93A6; }
  .qt-gear-btn {
    background: none; border: 1px solid rgba(255,255,255,0.12);
    color: #8A93A6; width: 24px; height: 24px; border-radius: 50%;
    font-size: 12px; cursor: pointer; display: flex; align-items: center; justify-content: center;
    padding: 0; line-height: 1;
  }
  .qt-gear-btn:hover { color: #4DE3FF; border-color: rgba(77,227,255,0.4); }
  .qt-gear-btn-danger:hover { color: #FF4D5E; border-color: rgba(255,77,94,0.4); }
  .qt-inline-confirm {
    font-size: 11.5px; color: #8A93A6; display: flex; align-items: center; gap: 6px;
  }
  .qt-inline-confirm-yes, .qt-inline-confirm-no {
    background: none; border: none; font-size: 11.5px; cursor: pointer; padding: 2px 4px;
    text-decoration: underline;
  }
  .qt-inline-confirm-yes { color: #FF4D5E; }
  .qt-inline-confirm-no { color: #7C8598; }

  .qt-timer-wrap {
    text-align: center;
    background: rgba(255,255,255,0.025);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 18px;
    padding: 24px 10px 18px;
    margin-bottom: 16px;
  }
  .qt-timer {
    font-family: "SF Mono", "Roboto Mono", Menlo, Consolas, monospace;
    font-size: 26px;
    font-weight: 600;
    letter-spacing: 0.02em;
    color: #F2F6FF;
    white-space: nowrap;
  }
  .qt-timer-colon { opacity: 0.35; padding: 0 2px; }
  .qt-timer-caption {
    margin-top: 8px; font-size: 10px; letter-spacing: 0.08em;
    color: #5C6479;
  }
  .qt-fail-pill {
    display: inline-block; margin-top: 14px;
    background: rgba(255,77,94,0.08);
    border: 1px solid rgba(255,77,94,0.25);
    color: #FF8B96;
    font-size: 12px;
    padding: 5px 14px;
    border-radius: 999px;
  }
  .qt-fail-pill b { color: #FF4D5E; }

  .qt-actions { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; margin-bottom: 14px; }
  .qt-btn {
    border: none; border-radius: 14px; padding: 15px 8px;
    font-size: 14px; font-weight: 600; cursor: pointer;
    color: #06110C;
    transition: transform .12s ease, box-shadow .2s ease;
  }
  .qt-btn:active { transform: scale(0.97); }
  .qt-btn-success {
    background: linear-gradient(180deg, #4CFFA0, #1FCF7A);
    box-shadow: 0 0 24px -6px rgba(57,255,136,0.55);
  }
  .qt-btn-fail {
    background: linear-gradient(180deg, #FF6270, #E5283A);
    color: #180507;
    box-shadow: 0 0 24px -6px rgba(255,40,58,0.5);
  }

  .qt-form {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 16px;
    padding: 16px;
    margin-bottom: 14px;
  }
  .qt-form-title { font-size: 13.5px; color: #C7CEDC; margin-bottom: 12px; font-weight: 500; }
  .qt-chips { display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 12px; }
  .qt-chip {
    border: 1px solid rgba(255,255,255,0.14);
    background: transparent;
    color: #9AA5B8;
    border-radius: 999px;
    padding: 7px 13px;
    font-size: 12px;
    cursor: pointer;
    transition: all .15s ease;
  }
  .qt-textarea {
    width: 100%;
    background: rgba(0,0,0,0.25);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 10px;
    color: #E7ECF5;
    padding: 10px 12px;
    font-size: 13.5px;
    font-family: inherit;
    resize: none;
    margin-bottom: 12px;
  }
  .qt-textarea:focus { outline: none; border-color: rgba(255,255,255,0.3); }
  .qt-textarea::placeholder { color: #5C6479; }
  .qt-form-actions { display: flex; justify-content: space-between; align-items: center; }
  .qt-link-btn {
    background: none; border: none; color: #7C8598;
    font-size: 12.5px; cursor: pointer; padding: 8px 4px;
  }
  .qt-link-btn:hover { color: #A9B2C3; }
  .qt-btn-small {
    border: none; border-radius: 10px; padding: 9px 18px;
    font-size: 13px; font-weight: 600; color: #06110C; cursor: pointer;
  }

  .qt-ai {
    background: rgba(77,227,255,0.05);
    border: 1px solid rgba(77,227,255,0.22);
    border-radius: 16px;
    padding: 16px 16px 17px;
    margin-bottom: 14px;
  }
  .qt-ai-warning {
    background: rgba(255,77,94,0.06);
    border-color: rgba(255,77,94,0.3);
  }
  .qt-ai-top { display: flex; align-items: center; gap: 7px; margin-bottom: 8px; }
  .qt-ai-dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: #4DE3FF;
    box-shadow: 0 0 8px #4DE3FF;
    animation: qtPulse 1.8s ease-in-out infinite;
  }
  .qt-ai-warning .qt-ai-dot { background: #FF4D5E; box-shadow: 0 0 8px #FF4D5E; }
  @keyframes qtPulse { 0%,100% { opacity: 0.4; } 50% { opacity: 1; } }
  .qt-ai-label { font-size: 10.5px; letter-spacing: 0.06em; color: #6E93A8; }
  .qt-ai-warning .qt-ai-label { color: #C77E85; }
  .qt-ai-title { font-size: 15px; font-weight: 600; margin-bottom: 6px; color: #F2F6FF; }
  .qt-ai-text { font-size: 13.5px; line-height: 1.6; color: #B7C0D1; margin: 0; }

  .qt-chart-card {
    background: rgba(255,255,255,0.025);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 16px;
    padding: 14px 14px 6px;
    margin-bottom: 14px;
  }
  .qt-chart-head { display: flex; align-items: center; justify-content: space-between; padding: 0 2px 6px; }
  .qt-chart-title { font-size: 12.5px; color: #A9B2C3; font-weight: 500; }
  .qt-chart-legend { display: flex; align-items: center; gap: 5px; font-size: 11.5px; color: #8A93A6; }
  .qt-legend-dot { width: 7px; height: 7px; border-radius: 50%; display: inline-block; }
  .qt-chart-body { margin: 0 -6px; }

  .qt-log-section {
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 16px;
    overflow: hidden;
  }
  .qt-log-toggle-row { display: flex; align-items: stretch; }
  .qt-log-toggle {
    flex: 1; background: rgba(255,255,255,0.02); border: none;
    color: #A9B2C3; font-size: 13px; padding: 14px 16px;
    display: flex; align-items: center; justify-content: space-between;
    cursor: pointer;
  }
  .qt-export-btn {
    background: none; border: none; border-left: 1px solid rgba(255,255,255,0.08);
    color: #6E93A8; font-size: 11.5px; padding: 0 16px; cursor: pointer;
  }
  .qt-export-btn:hover { color: #4DE3FF; }
  .qt-chevron { transition: transform .2s ease; color: #5C6479; }
  .qt-chevron-open { transform: rotate(180deg); }
  .qt-log-list { padding: 4px 16px 12px; }
  .qt-log-empty { color: #5C6479; font-size: 12.5px; padding: 10px 0; }
  .qt-log-row {
    display: flex; gap: 10px; padding: 10px 0;
    border-top: 1px solid rgba(255,255,255,0.05);
  }
  .qt-log-row:first-child { border-top: none; }
  .qt-log-icon { font-size: 14px; margin-top: 1px; }
  .qt-log-body { flex: 1; min-width: 0; }
  .qt-log-top { display: flex; align-items: center; gap: 8px; flex-wrap: wrap; }
  .qt-log-time { font-size: 11.5px; color: #6B7488; font-family: "SF Mono", Menlo, monospace; }
  .qt-log-tag {
    font-size: 10.5px; color: #9AA5B8;
    background: rgba(255,255,255,0.06);
    border-radius: 999px; padding: 2px 8px;
  }
  .qt-log-comment { font-size: 12.5px; color: #B7C0D1; margin-top: 3px; line-height: 1.4; }

  .qt-add-tile {
    width: 100%; margin-top: 18px;
    background: rgba(255,255,255,0.02);
    border: 1px dashed rgba(255,255,255,0.18);
    border-radius: 18px;
    color: #8A93A6;
    font-size: 13.5px; font-weight: 500;
    padding: 16px;
    cursor: pointer;
    transition: border-color .2s ease, color .2s ease;
  }
  .qt-add-tile:hover { border-color: rgba(77,227,255,0.4); color: #4DE3FF; }
  .qt-add-panel {
    margin-top: 18px;
    background: rgba(255,255,255,0.02);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 18px;
    padding: 16px;
    text-align: center;
  }
  .qt-add-panel .qt-type-grid { margin-bottom: 10px; }
  .qt-all-added {
    margin-top: 18px; text-align: center; font-size: 12.5px; color: #5C6479;
  }

  .qt-field-label {
    display: block; font-size: 12px; color: #8A93A6; margin-bottom: 12px;
  }
  .qt-input {
    display: block; width: 100%; margin-top: 6px;
    background: rgba(0,0,0,0.25); border: 1px solid rgba(255,255,255,0.12);
    border-radius: 8px; color: #E7ECF5; padding: 9px 10px; font-size: 14px;
    font-family: inherit;
  }
  .qt-input:focus { outline: none; border-color: rgba(77,227,255,0.5); }

  .qt-modal-backdrop {
    position: fixed; inset: 0; background: rgba(6,8,14,0.7);
    backdrop-filter: blur(2px);
    display: flex; align-items: center; justify-content: center;
    padding: 20px; z-index: 50;
  }
  .qt-modal {
    background: #10151F; border: 1px solid rgba(255,255,255,0.12);
    border-radius: 18px; padding: 22px; max-width: 340px; width: 100%;
  }
  .qt-modal-title { font-size: 16px; font-weight: 600; margin-bottom: 8px; }
  .qt-modal-text { font-size: 13px; color: #8A93A6; line-height: 1.5; margin: 0 0 18px; }
  .qt-modal-actions { display: flex; justify-content: flex-end; gap: 8px; align-items: center; }

  @media (max-width: 380px) {
    .qt-timer { font-size: 22px; }
  }
`;

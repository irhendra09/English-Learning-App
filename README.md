# English-Learning-App


<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Simple English Learning App</title>
<style>
  /* Reset and base */
  * {
    box-sizing: border-box;
  }

  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #f5f7fa;
    margin: 0;
    padding: 0;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: flex-start;
    color: #333;
  }

  header {
    width: 100%;
    max-width: 800px;
    padding: 1rem;
    text-align: center;
    background-color: #4a90e2;
    color: white;
    box-shadow: 0 2px 8px rgb(74 144 226 / 0.45);
  }

  header h1 {
    margin: 0;
    font-weight: 700;
    font-size: 1.8rem;
  }

  main {
    flex-grow: 1;
    width: 100%;
    max-width: 720px;
    padding: 1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .card {
    background: white;
    padding: 1.5rem 2rem;
    margin-top: 1rem;
    border-radius: 10px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.1);
    max-width: 600px;
    width: 100%;
    text-align: center;
  }

  .category-select {
    margin-bottom: 1rem;
    width: 100%;
    max-width: 300px;
    padding: 0.5rem 0.8rem;
    font-size: 1rem;
    border-radius: 8px;
    border: 1.8px solid #4a90e2;
    background: #f0f6ff;
    color: #333;
    cursor: pointer;
  }

  .search-container {
    margin-bottom: 1rem;
    width: 100%;
    max-width: 600px;
  }

  #searchInput {
    width: 100%;
    padding: 0.6rem 0.8rem;
    font-size: 1rem;
    border: 1.5px solid #ccc;
    border-radius: 8px;
    transition: border-color 0.25s;
  }
  #searchInput:focus {
    border-color: #4a90e2;
    outline: none;
  }

  .word-title {
    font-size: 2.4rem;
    font-weight: 700;
    margin-bottom: 0.2rem;
    color: #205081;
  }

  .meaning {
    font-size: 1.2rem;
    margin-bottom: 1rem;
    color: #666;
  }

  .sentence {
    font-style: italic;
    margin-bottom: 1.4rem;
    color: #444;
  }

  button {
    cursor: pointer;
    font-size: 1rem;
    padding: 0.5rem 1.3rem;
    margin: 0.2rem 0.5rem;
    border: none;
    border-radius: 7px;
    background-color: #4a90e2;
    color: white;
    box-shadow: 0 4px 10px rgb(74 144 226 / 0.5);
    transition: background-color 0.25s ease;
  }
  button:hover, button:focus {
    background-color: #357ABD;
    outline: none;
  }
  button:active {
    transform: scale(0.97);
  }

  .play-btn {
    font-size: 1.4rem;
    background-color: #7ec8f7;
    box-shadow: 0 3px 8px rgba(126,200,247,0.7);
  }
  .play-btn:hover {
    background-color: #3f99e6;
  }

  .favorite-btn {
    background-color: #e95b5b;
    box-shadow: 0 3px 8px rgba(233,91,91,0.7);
  }
  .favorite-btn.active {
    background-color: #b83f3f;
  }
  .favorite-btn:hover {
    background-color: #af4e4e;
  }

  .learned-indicator {
    margin-top: 0.7rem;
    font-size: 0.9rem;
    color: #3c763d;
  }

  /* Quiz styles */
  .quiz-container {
    margin-top: 2rem;
    background: white;
    padding: 1.6rem 2rem;
    border-radius: 10px;
    max-width: 600px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.1);
  }

  .quiz-question {
    font-weight: 600;
    font-size: 1.6rem;
    margin-bottom: 1rem;
    color: #205081;
  }

  .quiz-options {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .quiz-options li {
    background: #f5f9ff;
    border: 1.8px solid #4a90e2;
    border-radius: 8px;
    margin-bottom: 0.8rem;
    padding: 0.7rem 1.1rem;
    cursor: pointer;
    transition: background-color 0.3s;
  }

  .quiz-options li:hover {
    background-color: #d6e6fd;
  }

  .quiz-options li.correct {
    background-color: #c6f6c6;
    border-color: #33a533;
    color: #207320;
    cursor: default;
  }

  .quiz-options li.incorrect {
    background-color: #f8d7da;
    border-color: #c9302c;
    color: #721c24;
    cursor: default;
  }

  .quiz-feedback {
    margin-top: 1rem;
    font-size: 1.1rem;
    font-weight: 600;
  }

  @media (max-width: 480px) {
    .word-title {
      font-size: 1.8rem;
    }

    .meaning {
      font-size: 1.1rem;
    }

    .sentence {
      font-size: 0.95rem;
    }

    button {
      font-size: 0.9rem;
      padding: 0.45rem 1rem;
    }
  }
</style>
</head>
<body>
<header>
  <h1>English Learning App</h1>
</header>
<main>
  <select id="categorySelect" class="category-select" aria-label="Select vocabulary category"></select>

  <div class="search-container">
    <input type="search" id="searchInput" placeholder="Search word or meaning..." aria-label="Search words" />
  </div>

  <div class="card" role="region" aria-live="polite" aria-atomic="true">
    <div class="word-title" id="wordTitle">Word</div>
    <div class="meaning" id="wordMeaning">Meaning</div>
    <div class="sentence" id="wordSentence">Sample sentence</div>
    <button id="playBtn" class="play-btn" aria-label="Play pronunciation">🔊 Play</button>
    <button id="favoriteBtn" class="favorite-btn" aria-label="Mark as favorite">❤ Favorite</button>
    <div class="learned-indicator" id="learnedIndicator"></div>
  </div>

  <div style="margin-top: 1rem;">
    <button id="prevBtn" aria-label="Previous word">Previous Word</button>
    <button id="nextBtn" aria-label="Next word">Next Word</button>
    <button id="shuffleBtn" aria-label="Shuffle word">Shuffle</button>
    <button id="startQuizBtn" aria-label="Start quiz">Start Quiz</button>
  </div>

  <section class="quiz-container" id="quizSection" hidden>
    <div class="quiz-question" id="quizQuestion">Question?</div>
    <ul class="quiz-options" id="quizOptions"></ul>
    <div class="quiz-feedback" id="quizFeedback"></div>
    <button id="quitQuizBtn" style="margin-top:1rem; background:#777; box-shadow:none;">Quit Quiz</button>
  </section>
</main>

<script>
(() => {
  // Vocabulary data categorized by themes
  const vocabData = {
    general: [
      {
        word: "Example",
        meaning: "Contoh",
        sentence: "This is an example sentence to show usage.",
      },
    ],
    food: [
      {
        word: "Apple",
        meaning: "Apel",
        sentence: "I ate a red apple for breakfast.",
      },
      {
        word: "Bread",
        meaning: "Roti",
        sentence: "She bought fresh bread from the bakery.",
      },
      {
        word: "Cheese",
        meaning: "Keju",
        sentence: "He likes cheese on his sandwich.",
      },
    ],
    emotions: [
      {
        word: "Happy",
        meaning: "Senang",
        sentence: "She felt happy when she got the news.",
      },
      {
        word: "Angry",
        meaning: "Marah",
        sentence: "He was angry because he lost the game.",
      },
      {
        word: "Surprised",
        meaning: "Terkejut",
        sentence: "I was surprised by the birthday party.",
      },
    ],
    jobs: [
      {
        word: "Teacher",
        meaning: "Guru",
        sentence: "My sister is a high school teacher.",
      },
      {
        word: "Doctor",
        meaning: "Dokter",
        sentence: "The doctor helped the injured man.",
      },
      {
        word: "Engineer",
        meaning: "Insinyur",
        sentence: "He works as a civil engineer.",
      },
    ]
  };

  // Flattened list for searching and quiz
  let wordList = [];
  let currentCategory = '';
  let filteredList = [];
  let currentIndex = 0;

  // DOM elements
  const categorySelect = document.getElementById('categorySelect');
  const searchInput = document.getElementById('searchInput');
  const wordTitle = document.getElementById('wordTitle');
  const wordMeaning = document.getElementById('wordMeaning');
  const wordSentence = document.getElementById('wordSentence');
  const playBtn = document.getElementById('playBtn');
  const favoriteBtn = document.getElementById('favoriteBtn');
  const learnedIndicator = document.getElementById('learnedIndicator');
  const prevBtn = document.getElementById('prevBtn');
  const nextBtn = document.getElementById('nextBtn');
  const shuffleBtn = document.getElementById('shuffleBtn');
  const startQuizBtn = document.getElementById('startQuizBtn');
  const quizSection = document.getElementById('quizSection');
  const quizQuestion = document.getElementById('quizQuestion');
  const quizOptions = document.getElementById('quizOptions');
  const quizFeedback = document.getElementById('quizFeedback');
  const quitQuizBtn = document.getElementById('quitQuizBtn');

  // localStorage keys
  const LS_LEARNED_KEY = 'learnedWords';
  const LS_FAVORITE_KEY = 'favoriteWords';

  // Load learned and favorite words from localStorage
  let learnedWords = new Set(JSON.parse(localStorage.getItem(LS_LEARNED_KEY)) || []);
  let favoriteWords = new Set(JSON.parse(localStorage.getItem(LS_FAVORITE_KEY)) || []);

  // Helper functions
  function saveLearnedWords() {
    localStorage.setItem(LS_LEARNED_KEY, JSON.stringify([...learnedWords]));
  }

  function saveFavoriteWords() {
    localStorage.setItem(LS_FAVORITE_KEY, JSON.stringify([...favoriteWords]));
  }

  // Populate category dropdown
  function populateCategorySelect() {
    categorySelect.innerHTML = '';
    const defaultOption = document.createElement('option');
    defaultOption.value = '';
    defaultOption.textContent = '-- Select a category --';
    categorySelect.appendChild(defaultOption);

    Object.keys(vocabData).forEach(category => {
      const option = document.createElement('option');
      option.value = category;
      // Capitalize first letter
      option.textContent = category.charAt(0).toUpperCase() + category.slice(1);
      categorySelect.appendChild(option);
    });
  }

  // Load word list by category
  function loadWordList(category) {
    currentCategory = category;
    if (category && vocabData[category]) {
      wordList = vocabData[category].slice();
    } else {
      // If no category, combine all words (flatten)
      wordList = [];
      Object.values(vocabData).forEach(arr => wordList.push(...arr));
    }
    currentIndex = 0;
    filteredList = wordList.slice();
    searchInput.value = '';
  }

  // Display current word details
  function displayCurrentWord() {
    if (filteredList.length === 0) {
      wordTitle.textContent = 'No words found';
      wordMeaning.textContent = '';
      wordSentence.textContent = '';
      learnedIndicator.textContent = '';
      favoriteBtn.classList.remove('active');
      playBtn.disabled = true;
      favoriteBtn.disabled = true;
      return;
    }

    const wordObj = filteredList[currentIndex];
    wordTitle.textContent = wordObj.word;
    wordMeaning.textContent = `Meaning: ${wordObj.meaning}`;
    wordSentence.textContent = `Example: ${wordObj.sentence}`;
    playBtn.disabled = false;
    favoriteBtn.disabled = false;

    // Mark learned if word is in learnedWords
    if (learnedWords.has(wordObj.word)) {
      learnedIndicator.textContent = '✔ Learned';
    } else {
      learnedIndicator.textContent = '';
    }

    // Mark favorite button active if favorite
    if (favoriteWords.has(wordObj.word)) {
      favoriteBtn.classList.add('active');
      favoriteBtn.textContent = '❤ Favorited';
    } else {
      favoriteBtn.classList.remove('active');
      favoriteBtn.textContent = '❤ Favorite';
    }
  }

  // Play pronunciation using TTS
  function playPronunciation() {
    if (filteredList.length === 0) return;
    const word = filteredList[currentIndex].word;
    if ('speechSynthesis' in window) {
      const utterance = new SpeechSynthesisUtterance(word);
      utterance.lang = 'en-US';
      window.speechSynthesis.speak(utterance);
    } else {
      alert('Sorry, your browser does not support Text-to-Speech.');
    }
  }

  // Navigate helpers
  function nextWord() {
    if (filteredList.length === 0) return;
    currentIndex = (currentIndex + 1) % filteredList.length;
    displayCurrentWord();
  }
  function prevWord() {
    if (filteredList.length === 0) return;
    currentIndex = (currentIndex - 1 + filteredList.length) % filteredList.length;
    displayCurrentWord();
  }
  function shuffleWord() {
    if (filteredList.length === 0) return;
    if (filteredList.length === 1) {
      currentIndex = 0;
    } else {
      let newIndex = currentIndex;
      while (newIndex === currentIndex) {
        newIndex = Math.floor(Math.random() * filteredList.length);
      }
      currentIndex = newIndex;
    }
    displayCurrentWord();
  }

  // Search words by word or meaning substring case insensitive
  function searchWords(term) {
    const lowerTerm = term.trim().toLowerCase();
    if (!lowerTerm) {
      filteredList = wordList.slice();
    } else {
      filteredList = wordList.filter(item => 
        item.word.toLowerCase().includes(lowerTerm) ||
        item.meaning.toLowerCase().includes(lowerTerm) ||
        item.sentence.toLowerCase().includes(lowerTerm)
      );
    }
    currentIndex = 0;
    displayCurrentWord();
  }

  // Toggle favorite state for the current word
  function toggleFavorite() {
    if (filteredList.length === 0) return;
    const word = filteredList[currentIndex].word;
    if (favoriteWords.has(word)) {
      favoriteWords.delete(word);
    } else {
      favoriteWords.add(word);
      // Mark word as learned too once favorited
      learnedWords.add(word);
      saveLearnedWords();
      learnedIndicator.textContent = '✔ Learned';
    }
    saveFavoriteWords();
    displayCurrentWord();
  }

  // =================== Quiz Feature =====================

  let quizActive = false;
  let quizWords = [];
  let quizCurrentIndex = 0;
  let quizScore = 0;

  // Generate quiz data with shuffled multiple choice
  function generateQuiz() {
    quizWords = filteredList.length ? filteredList.slice() : wordList.slice();
    if (quizWords.length < 4) {
      alert('Not enough words to start the quiz (minimum 4).');
      return false;
    }

    quizScore = 0;
    quizCurrentIndex = 0;
    quizActive = true;
    quizSection.hidden = false;
    startQuizBtn.disabled = true;
    prevBtn.disabled = true;
    nextBtn.disabled = true;
    shuffleBtn.disabled = true;
    categorySelect.disabled = true;
    searchInput.disabled = true;
    favoriteBtn.disabled = true;
    playBtn.disabled = true;

    // Shuffle quizWords to random order
    for (let i = quizWords.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [quizWords[i], quizWords[j]] = [quizWords[j], quizWords[i]];
    }

    showQuizQuestion();

    return true;
  }

  // Show quiz question and answer options
  function showQuizQuestion() {
    quizFeedback.textContent = '';
    if (quizCurrentIndex >= quizWords.length) {
      showQuizResults();
      return;
    }

    const currentWord = quizWords[quizCurrentIndex];
    quizQuestion.textContent = `What is the meaning of "${currentWord.word}"?`;

    // Prepare options, including correct + 3 random wrong meanings
    const meaningsPool = new Set();
    meaningsPool.add(currentWord.meaning);

    while (meaningsPool.size < 4) {
      const randomWord = wordList[Math.floor(Math.random() * wordList.length)];
      if (randomWord.meaning !== currentWord.meaning) {
        meaningsPool.add(randomWord.meaning);
      }
    }

    const optionsArray = Array.from(meaningsPool);
    // Shuffle options
    for (let i = optionsArray.length -1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [optionsArray[i], optionsArray[j]] = [optionsArray[j], optionsArray[i]];
    }

    quizOptions.innerHTML = '';
    optionsArray.forEach(option => {
      const li = document.createElement('li');
      li.tabIndex = 0;
      li.textContent = option;
      li.setAttribute('role', 'button');
      li.addEventListener('click', () => handleQuizAnswer(li, option, currentWord.meaning));
      li.addEventListener('keydown', (e) => {
        if (e.key === 'Enter' || e.key === ' ') {
          e.preventDefault();
          li.click();
        }
      });
      quizOptions.appendChild(li);
    });
  }

  // Handle quiz answer selection
  function handleQuizAnswer(liElem, selectedMeaning, correctMeaning) {
    if (!quizActive) return;

    // Disable all options
    Array.from(quizOptions.children).forEach(opt => {
      opt.style.pointerEvents = 'none';
    });

    if (selectedMeaning === correctMeaning) {
      liElem.classList.add('correct');
      quizScore++;
      quizFeedback.textContent = 'Correct! ✔';
      // Mark current word as learned
      learnedWords.add(quizWords[quizCurrentIndex].word);
      saveLearnedWords();
    } else {
      liElem.classList.add('incorrect');
      quizFeedback.textContent = `Wrong ✘ The correct meaning is "${correctMeaning}".`;
      // Highlight correct option
      Array.from(quizOptions.children).forEach(opt => {
        if (opt.textContent === correctMeaning) {
          opt.classList.add('correct');
        }
      });
    }

    quizCurrentIndex++;
    // Show next question after short delay
    setTimeout(() => {
      if (quizCurrentIndex < quizWords.length) {
        showQuizQuestion();
      } else {
        showQuizResults();
      }
    }, 1500);
  }

  // Show quiz results and reset UI
  function showQuizResults() {
    quizFeedback.textContent = `Quiz ended. Your score: ${quizScore} / ${quizWords.length}`;
    quizActive = false;

    // Re-enable UI controls
    startQuizBtn.disabled = false;
    prevBtn.disabled = false;
    nextBtn.disabled = false;
    shuffleBtn.disabled = false;
    categorySelect.disabled = false;
    searchInput.disabled = false;
    favoriteBtn.disabled = false;
    playBtn.disabled = false;
  }

  // Quit quiz and reset UI
  function quitQuiz() {
    quizActive = false;
    quizSection.hidden = true;
    quizOptions.innerHTML = '';
    quizFeedback.textContent = '';
    startQuizBtn.disabled = false;
    prevBtn.disabled = false;
    nextBtn.disabled = false;
    shuffleBtn.disabled = false;
    categorySelect.disabled = false;
    searchInput.disabled = false;
    favoriteBtn.disabled = false;
    playBtn.disabled = false;
  }

  // Event Listeners
  categorySelect.addEventListener('change', e => {
    loadWordList(e.target.value);
    displayCurrentWord();
  });

  searchInput.addEventListener('input', e => {
    searchWords(e.target.value);
  });

  playBtn.addEventListener('click', () => {
    playPronunciation();
  });

  favoriteBtn.addEventListener('click', () => {
    toggleFavorite();
  });

  nextBtn.addEventListener('click', () => {
    nextWord();
  });

  prevBtn.addEventListener('click', () => {
    prevWord();
  });

  shuffleBtn.addEventListener('click', () => {
    shuffleWord();
  });

  startQuizBtn.addEventListener('click', () => {
    generateQuiz();
  });

  quitQuizBtn.addEventListener('click', () => {
    quitQuiz();
  });

  // Initialization
  function init() {
    populateCategorySelect();
    loadWordList('');
    displayCurrentWord();
  }

  init();
})();
</script>
</body>
</html>


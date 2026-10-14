
const taskCheckboxes = document.querySelectorAll(
  '.task-item input[type="checkbox"]'
);

const progressFill = document.querySelector('.progress-fill');
const progressNumber = document.querySelector('.progress-heading strong');
const progressMessage = document.querySelector('.progress-panel small');

function updateProgress() {
  const total = taskCheckboxes.length;
  const completed = [...taskCheckboxes].filter(task => task.checked).length;
  const percent = Math.round((completed / total) * 100);

  progressFill.style.width = percent + '%';
  progressNumber.textContent = percent + '%';

  if (percent === 100) {
    progressMessage.textContent = 'Amazing! All demo tasks completed 🎉';
  } else if (percent > 0) {
    progressMessage.textContent = 'Nice work! Keep the momentum going ✨';
  } else {
    progressMessage.textContent = "You're building a great habit ✨";
  }
}

taskCheckboxes.forEach(task => {
  task.addEventListener('change', updateProgress);
});

updateProgress();


const taskInput = document.getElementById('taskInput');
const addTaskButton = document.getElementById('addTask');
const taskList = document.getElementById('taskList');
let savedTasks = JSON.parse(
  localStorage.getItem('studentSaathiTasks') || '[]'
);

addTaskButton.addEventListener('click', function () {
  const taskText = taskInput.value.trim();

  if (taskText === '') {
    taskInput.focus();
    return;
  }

  const taskItem = document.createElement('li');
  const taskCheckbox = document.createElement('input');
  const taskLabel = document.createElement('span');
  const deleteButton = document.createElement('button');

  taskCheckbox.type = 'checkbox';
  taskLabel.textContent = taskText;
  deleteButton.textContent = 'Delete';

  taskCheckbox.addEventListener('change', function () {
    taskLabel.style.textDecoration =
      taskCheckbox.checked ? 'line-through' : 'none';
  });

  deleteButton.addEventListener('click', function () {
    taskItem.remove();
    saveTasks();
  });

  taskItem.append(taskCheckbox, taskLabel, deleteButton);
  taskList.appendChild(taskItem);
  saveTasks();

  taskInput.value = '';
  taskInput.focus();
});
function saveTasks() {
  localStorage.setItem(
    'studentSaathiTasks',
    JSON.stringify(
      Array.from(taskList.children).map(function(item) {
        return {
          text: item.querySelector('span').textContent,
          completed: item.querySelector('input').checked
        };
      })
    )
  );
}

function loadTasks() {
  const saved = JSON.parse(
    localStorage.getItem('studentSaathiTasks') || '[]'
  );

  saved.forEach(function(task) {
    const taskItem = document.createElement('li');

    const taskCheckbox = document.createElement('input');
    taskCheckbox.type = 'checkbox';
    taskCheckbox.checked = task.completed;

    const taskLabel = document.createElement('span');
    taskLabel.textContent = task.text;
    taskLabel.style.textDecoration =
      task.completed ? 'line-through' : 'none';

    const deleteButton = document.createElement('button');
    deleteButton.textContent = 'Delete';

    taskCheckbox.addEventListener('change', function() {
      taskLabel.style.textDecoration =
        taskCheckbox.checked ? 'line-through' : 'none';
      saveTasks();
    });

    deleteButton.addEventListener('click', function() {
      taskItem.remove();
      saveTasks();
    });

    taskItem.append(taskCheckbox, taskLabel, deleteButton);
    taskList.appendChild(taskItem);
  });
}

loadTasks();

function updateTaskProgress() {
  const checkboxes = document.querySelectorAll(
    '#taskList input[type="checkbox"]'
  );

  const total = checkboxes.length;
  const completed = Array.from(checkboxes).filter(
    checkbox => checkbox.checked
  ).length;

  document.getElementById('totalTaskCount').textContent = total;
  document.getElementById('completedTaskCount').textContent = completed;
  document.getElementById('pendingTaskCount').textContent =
    total - completed;
}

const taskProgressObserver = new MutationObserver(updateTaskProgress);

taskProgressObserver.observe(
  document.getElementById('taskList'),
  { childList: true, subtree: true, attributes: true }
);

document.getElementById('taskList').addEventListener(
  'change',
  updateTaskProgress
);

updateTaskProgress();

let focusTime = 30 * 60;
let timerInterval = null;

const timerDisplay = document.getElementById("timerDisplay");
const startButton = document.getElementById("startTimer");
const pauseButton = document.getElementById("pauseTimer");
const resetButton = document.getElementById("resetTimer");
const timerMessage = document.getElementById("timerMessage");

function showTime() {
  const minutes = Math.floor(focusTime / 60);
  const seconds = focusTime % 60;

  timerDisplay.textContent =
    String(minutes).padStart(2, "0") + ":" +
    String(seconds).padStart(2, "0");
}

startButton.addEventListener("click", function () {
  if (timerInterval !== null) return;

  if (focusTime <= 0) {
    timerMessage.textContent = "Timer reset karo aur phir start karo!";
    return;
  }

  timerMessage.textContent = "Stay focused! You can do it 🚀";

  timerInterval = setInterval(function () {
    focusTime--;
    showTime();

    if (focusTime <= 0) {
      clearInterval(timerInterval);
      timerInterval = null;
      timerMessage.textContent = "Session complete! Great work 🎉";
    }
  }, 1000);
});

pauseButton.addEventListener("click", function () {
  clearInterval(timerInterval);
  timerInterval = null;
  timerMessage.textContent = "Timer paused. Take a breath.";
});

resetButton.addEventListener("click", function () {
  clearInterval(timerInterval);
  timerInterval = null;
  focusTime = 30 * 60;
  showTime();
  timerMessage.textContent = "Ready when you are ✨";
});

showTime();

let breakTime = 5 * 60;
let breakInterval = null;

const breakDisplay = document.getElementById("breakDisplay");
const startBreakButton = document.getElementById("startBreak");
const resetBreakButton = document.getElementById("resetBreak");
const breakMessage = document.getElementById("breakMessage");

function showBreakTime() {
  const minutes = Math.floor(breakTime / 60);
  const seconds = breakTime % 60;

  breakDisplay.textContent =
    String(minutes).padStart(2, "0") + ":" +
    String(seconds).padStart(2, "0");
}

function playBreakSound() {
  try {
    const audio = new AudioContext();
    const oscillator = audio.createOscillator();
    const volume = audio.createGain();

    oscillator.connect(volume);
    volume.connect(audio.destination);
    oscillator.frequency.value = 880;
    volume.gain.value = 0.15;

    oscillator.start();
    oscillator.stop(audio.currentTime + 0.6);
    oscillator.onended = function () {
      audio.close();
    };
  } catch (error) {
    breakMessage.textContent =
      "Break complete! 🎉 (Sound unavailable)";
  }
}

startBreakButton.addEventListener("click", function () {
  if (breakInterval !== null || breakTime <= 0) return;

  breakMessage.textContent = "Relax and recharge ☕";

  breakInterval = setInterval(function () {
    breakTime--;
    showBreakTime();

    if (breakTime <= 0) {
      clearInterval(breakInterval);
      breakInterval = null;
      breakMessage.textContent = "Break complete! Back to focus 🚀";
      playBreakSound();
    }
  }, 1000);
});

resetBreakButton.addEventListener("click", function () {
  clearInterval(breakInterval);
  breakInterval = null;
  breakTime = 5 * 60;
  showBreakTime();
  breakMessage.textContent = "Your break is ready when you are.";
});

showBreakTime();

const noteTitle = document.getElementById("noteTitle");
const noteContent = document.getElementById("noteContent");
const saveNoteButton = document.getElementById("saveNote");
const notesList = document.getElementById("notesList");
const notesMessage = document.getElementById("notesMessage");

let savedNotes = JSON.parse(
  localStorage.getItem("studentSaathiNotes") || "[]"
);

function renderNotes() {
  notesList.innerHTML = "";

  savedNotes.forEach(function(note, index) {
    const card = document.createElement("article");
    card.className = "note-card";

    const heading = document.createElement("h3");
    heading.textContent = note.title;

    const content = document.createElement("p");
    content.textContent = note.content;

    const deleteButton = document.createElement("button");
    deleteButton.textContent = "Delete";

    deleteButton.addEventListener("click", function() {
      savedNotes.splice(index, 1);

      localStorage.setItem(
        "studentSaathiNotes",
        JSON.stringify(savedNotes)
      );

      renderNotes();
      notesMessage.textContent = "Note deleted.";
    });

    card.append(heading, content, deleteButton);
    notesList.appendChild(card);
  });
}

saveNoteButton.addEventListener("click", function() {
  const title = noteTitle.value.trim();
  const content = noteContent.value.trim();

  if (!title || !content) {
    notesMessage.textContent = "Please enter both title and notes.";
    return;
  }

  savedNotes.unshift({ title: title, content: content });

  localStorage.setItem(
    "studentSaathiNotes",
    JSON.stringify(savedNotes)
  );

  noteTitle.value = "";
  noteContent.value = "";

  renderNotes();
  notesMessage.textContent = "Note saved successfully! 🎉";
});

renderNotes();

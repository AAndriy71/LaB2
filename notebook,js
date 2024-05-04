// Клас Note
class Note {
    constructor(id, title, content) {
        this.id = id;
        this.title = title;
        this.content = content;
        this.creationDate = new Date();
        this.reminder = null; // Текстове нагадування
        this.noteElement = null; // Зберігає посилання на DOM-елемент
    }

    updateContent(newContent) {
        this.content = newContent;
        this.updateNoteUI();
    }

    setReminder(reminder) {
        this.reminder = reminder;
        this.updateNoteUI();
    }

    clearReminder() {
        this.reminder = null;
        this.updateNoteUI();
    }

    editReminder(newReminder) {
        this.reminder = newReminder;
        this.updateNoteUI();
    }

    // Функція для відображення нотатки на сторінці
    render() {
        const noteDiv = document.createElement('div');
        noteDiv.classList.add('note');
        noteDiv.innerHTML = `<h3>${this.title}</h3><p>${this.content}</p>`;
        if (this.reminder) {
            noteDiv.innerHTML += `<p class="reminder">Нагадування: ${this.reminder}</p>`;
            noteDiv.innerHTML += `<p class="date">Дата додавання: ${this.creationDate.toLocaleString()}</p>`;
        }
        noteDiv.addEventListener('dblclick', () => {
            const newContent = prompt("Введіть новий текст нотатки:", this.content);
            if (newContent !== null) {
                this.updateContent(newContent);
            }
        });
        const reminderButton = document.createElement('button');
        reminderButton.textContent = this.reminder ? 'Видалити нагадування' : 'Додати';
        reminderButton.addEventListener('click', () => {
            if (this.reminder) {
                const newReminder = prompt("Введіть нове нагадування:", this.reminder);
                if (newReminder !== null) {
                    this.editReminder(newReminder);
                }
            } else {
                const reminder = prompt("Введіть нагадування:");
                if (reminder) {
                    this.setReminder(reminder);
                }
            }
        });
        noteDiv.appendChild(reminderButton);

        // Зберегти посилання на DOM-елемент
        this.noteElement = noteDiv;

        return noteDiv;
    }

    // Функція для оновлення відображення нотатки на сторінці
    updateNoteUI() {
        // Видалити старий елемент
        if (this.noteElement && this.noteElement.parentNode) {
            this.noteElement.parentNode.removeChild(this.noteElement);
        }

        // Оновити елемент з новим вмістом
        const updatedNoteElement = this.render();
        // Перед вставкою нового елемента, додайте йому id, щоб забезпечити можливість його знаходження
        updatedNoteElement.id = `note-${this.id}`;
        // Вставити новий елемент
        const notesContainer = document.getElementById('notes');
        notesContainer.appendChild(updatedNoteElement);
    }
}

// Клас Notebook
class Notebook {
    constructor() {
        this.notes = [];
    }

    addNote(note) {
        this.notes.push(note);
        this.renderNotes(); // Після додавання нотатки відображаємо всі нотатки
    }

    removeNote(noteId) {
        this.notes = this.notes.filter(note => note.id !== noteId);
        this.renderNotes(); // Після видалення нотатки оновлюємо список нотаток
    }

    clearNotes() {
        this.notes = [];
        this.renderNotes(); // Очищаємо сторінку
    }

    renderNotes() {
        const notesContainer = document.getElementById('notes');
        notesContainer.innerHTML = ''; // Очищаємо контейнер перед відображенням нових нотаток
        this.notes.forEach(note => {
            const noteElement = note.render();
            noteElement.id = `note-${note.id}`;
            notesContainer.appendChild(noteElement);
        });
    }
}

// Створення об'єкту Notebook
const notebook = new Notebook();

// Приклад використання
const note1 = new Note(1, "", "");
const note2 = new Note(2, "", "");

notebook.addNote(note1);
notebook.addNote(note2);

// Приклад очищення сторінки від нагадувань
const clearButton = document.createElement('button');
clearButton.textContent = 'Очистити сторінку';
clearButton.addEventListener('click', () => {
    notebook.clearNotes();
});
document.body.appendChild(clearButton);

// Приклад додавання нової нотатки
const addButton = document.createElement('button');
addButton.textContent = 'Додати нову нотатку';
addButton.addEventListener('click', () => {
    const newNote = new Note(
        notebook.notes.length + 1,
        "Нова нотатка",
        "Текст нової нотатки"
    );
    notebook.addNote(newNote);
});
document.body.appendChild(addButton);



# OnlineQuiz
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Online Quiz Maker</title>
    <style>
        :root {
            --primary-color: #3498db;
            --secondary-color: #2ecc71;
            --error-color: #e74c3c;
            --text-color: #333;
            --light-bg: #f9f9f9;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--light-bg);
            color: var(--text-color);
            line-height: 1.6;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        h1, h2, h3 {
            margin-bottom: 15px;
        }
        
        button {
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 10px 15px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            margin: 10px 5px;
            transition: background-color 0.3s;
        }
        
        button:hover {
            background-color: #2980b9;
        }
        
        button.secondary {
            background-color: var(--secondary-color);
        }
        
        button.secondary:hover {
            background-color: #27ae60;
        }
        
        button.danger {
            background-color: var(--error-color);
        }
        
        button.danger:hover {
            background-color: #c0392b;
        }
        
        .form-group {
            margin-bottom: 15px;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        
        input[type="text"],
        input[type="password"],
        input[type="email"],
        textarea,
        select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 16px;
        }
        
        .quiz-list {
            list-style: none;
        }
        
        .quiz-item {
            background: white;
            border-radius: 4px;
            padding: 15px;
            margin-bottom: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        
        .options {
            list-style-type: none;
            margin: 10px 0;
        }
        
        .option-item {
            background: white;
            border: 1px solid #ddd;
            border-radius: 4px;
            padding: 10px;
            margin-bottom: 10px;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .option-item:hover {
            background-color: #f4f4f4;
        }
        
        .option-item.selected {
            background-color: #e0f2f7;
            border-color: var(--primary-color);
        }
        
        .correct-answer {
            background-color: #d4edda !important;
            border-color: #28a745 !important;
        }
        
        .wrong-answer {
            background-color: #f8d7da !important;
            border-color: #dc3545 !important;
        }
        
        .result-item {
            margin-bottom: 10px;
            padding: 10px;
            border-radius: 4px;
        }
        
        .success-message {
            background-color: #d4edda;
            color: #155724;
            padding: 10px;
            margin-bottom: 15px;
            border-radius: 4px;
        }
        
        .error-message {
            background-color: #f8d7da;
            color: #721c24;
            padding: 10px;
            margin-bottom: 15px;
            border-radius: 4px;
        }
        
        .nav-bar {
            background-color: var(--primary-color);
            color: white;
            padding: 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .nav-bar a {
            color: white;
            text-decoration: none;
            margin: 0 10px;
        }
        
        .nav-bar .app-title {
            font-weight: bold;
            font-size: 1.2em;
        }
        
        .section {
            display: none;
        }
        
        .section.active {
            display: block;
        }
        
        .question-container {
            margin-bottom: 20px;
        }
        
        .add-option-btn {
            background-color: #95a5a6;
            margin-top: 10px;
        }
        
        .remove-btn {
            background-color: var(--error-color);
            margin-left: 10px;
        }
        
        .answer-feedback {
            font-weight: bold;
            margin-top: 10px;
        }
        
        @media (max-width: 768px) {
            .container {
                padding: 10px;
            }
            
            button {
                width: 100%;
                margin: 5px 0;
            }
            
            .nav-bar {
                flex-direction: column;
                text-align: center;
            }
            
            .nav-links {
                margin-top: 10px;
            }
        }
    </style>
</head>
<body>
    <div class="nav-bar">
        <span class="app-title">Online Quiz Maker</span>
        <div class="nav-links">
            <a href="#" id="home-link">Home</a>
            <a href="#" id="browse-quizzes-link">Browse Quizzes</a>
            <a href="#" id="user-profile-link">Profile</a>
            <span id="auth-links">
                <a href="#" id="login-link">Login</a>
                <a href="#" id="register-link">Register</a>
            </span>
            <a href="#" id="logout-link" style="display: none;">Logout</a>
        </div>
    </div>

    <div class="container">
        <!-- Home Section -->
        <section id="home-section" class="section active">
            <header>
                <h1>Welcome to Online Quiz Maker</h1>
                <p>Create, share, and take quizzes on any topic!</p>
            </header>
            <div class="home-buttons">
                <button id="create-quiz-btn">Create a Quiz</button>
                <button id="take-quiz-btn" class="secondary">Take a Quiz</button>
            </div>
        </section>

        <!-- User Authentication Section -->
        <section id="register-section" class="section">
            <h2>Create an Account</h2>
            <form id="register-form">
                <div class="form-group">
                    <label for="register-username">Username:</label>
                    <input type="text" id="register-username" required>
                </div>
                <div class="form-group">
                    <label for="register-email">Email:</label>
                    <input type="email" id="register-email" required>
                </div>
                <div class="form-group">
                    <label for="register-password">Password:</label>
                    <input type="password" id="register-password" required>
                </div>
                <div class="form-group">
                    <label for="register-confirm-password">Confirm Password:</label>
                    <input type="password" id="register-confirm-password" required>
                </div>
                <button type="submit">Register</button>
                <button type="button" class="secondary" id="go-to-login-btn">Already have an account? Login</button>
            </form>
            <div id="register-message"></div>
        </section>

        <section id="login-section" class="section">
            <h2>Login to Your Account</h2>
            <form id="login-form">
                <div class="form-group">
                    <label for="login-username">Username:</label>
                    <input type="text" id="login-username" required>
                </div>
                <div class="form-group">
                    <label for="login-password">Password:</label>
                    <input type="password" id="login-password" required>
                </div>
                <button type="submit">Login</button>
                <button type="button" class="secondary" id="go-to-register-btn">Don't have an account? Register</button>
            </form>
            <div id="login-message"></div>
        </section>

        <!-- Quiz Creation Section -->
        <section id="create-quiz-section" class="section">
            <h2>Create a New Quiz</h2>
            <form id="create-quiz-form">
                <div class="form-group">
                    <label for="quiz-title">Quiz Title:</label>
                    <input type="text" id="quiz-title" required>
                </div>
                <div class="form-group">
                    <label for="quiz-description">Description:</label>
                    <textarea id="quiz-description" rows="3" required></textarea>
                </div>
                
                <h3>Questions</h3>
                <div id="questions-container">
                    <!-- Question template will be added dynamically -->
                </div>
                
                <button type="button" id="add-question-btn">Add Question</button>
                <button type="submit">Create Quiz</button>
                <button type="button" class="secondary" id="cancel-create-quiz">Cancel</button>
            </form>
            <div id="create-quiz-message"></div>
        </section>

        <!-- Quiz Listing Section -->
        <section id="browse-quizzes-section" class="section">
            <h2>Available Quizzes</h2>
            <div id="quizzes-container">
                <ul id="quiz-list" class="quiz-list">
                    <!-- Quiz items will be added dynamically -->
                </ul>
            </div>
            <div id="no-quizzes-message" style="display: none;">
                <p>No quizzes available yet. Be the first to create one!</p>
                <button id="create-first-quiz-btn">Create a Quiz</button>
            </div>
        </section>

        <!-- Quiz Taking Section -->
        <section id="take-quiz-section" class="section">
            <h2 id="taking-quiz-title"></h2>
            <p id="taking-quiz-description"></p>
            
            <div id="quiz-progress">Question <span id="current-question-num">1</span> of <span id="total-questions"></span></div>
            
            <div id="question-container">
                <!-- Current question will be displayed here -->
            </div>
            
            <button id="next-question-btn">Next Question</button>
            <button id="submit-quiz-btn" style="display: none;">Submit Quiz</button>
            <button id="exit-quiz-btn" class="danger">Exit Quiz</button>
        </section>

        <!-- Quiz Results Section -->
        <section id="quiz-results-section" class="section">
            <h2>Quiz Results</h2>
            <div id="score-container">
                <h3>Your Score: <span id="quiz-score"></span> / <span id="quiz-total"></span></h3>
                <p>Percentage: <span id="score-percentage"></span>%</p>
            </div>
            
            <h3>Review Your Answers</h3>
            <div id="results-container">
                <!-- Results will be added dynamically -->
            </div>
            
            <button id="back-to-quizzes-btn">Back to All Quizzes</button>
            <button id="retake-quiz-btn">Retake This Quiz</button>
        </section>

        <!-- User Profile Section -->
        <section id="user-profile-section" class="section">
            <h2>Your Profile</h2>
            <div id="profile-info">
                <p><strong>Username:</strong> <span id="profile-username"></span></p>
                <p><strong>Email:</strong> <span id="profile-email"></span></p>
            </div>
            
            <h3>Your Quizzes</h3>
            <ul id="user-quizzes" class="quiz-list">
                <!-- User's quizzes will be added dynamically -->
            </ul>
            <div id="no-user-quizzes-message" style="display: none;">
                <p>You haven't created any quizzes yet.</p>
                <button id="create-user-quiz-btn">Create Your First Quiz</button>
            </div>
            
            <h3>Quizzes You've Taken</h3>
            <ul id="taken-quizzes" class="quiz-list">
                <!-- Taken quizzes will be added dynamically -->
            </ul>
            <div id="no-taken-quizzes-message" style="display: none;">
                <p>You haven't taken any quizzes yet.</p>
                <button id="browse-to-take-btn">Browse Quizzes to Take</button>
            </div>
        </section>
    </div>

    <script>
        // Data Storage Utilities
        const StorageUtil = {
            getItem: (key) => {
                const item = localStorage.getItem(key);
                return item ? JSON.parse(item) : null;
            },
            setItem: (key, value) => {
                localStorage.setItem(key, JSON.stringify(value));
            },
            removeItem: (key) => {
                localStorage.removeItem(key);
            },
            getQuizzes: () => StorageUtil.getItem('quizzes') || [],
            saveQuizzes: (quizzes) => StorageUtil.setItem('quizzes', quizzes),
            getUsers: () => StorageUtil.getItem('users') || [],
            saveUsers: (users) => StorageUtil.setItem('users', users),
            getCurrentUser: () => StorageUtil.getItem('currentUser'),
            setCurrentUser: (user) => StorageUtil.setItem('currentUser', user),
            logoutUser: () => StorageUtil.removeItem('currentUser'),
            getQuizResults: () => StorageUtil.getItem('quizResults') || [],
            saveQuizResults: (results) => StorageUtil.setItem('quizResults', results)
        };

        // Navigation Utilities
        const NavUtil = {
            showSection: (sectionId) => {
                document.querySelectorAll('.section').forEach(section => {
                    section.classList.remove('active');
                });
                document.getElementById(sectionId).classList.add('active');
            },
            updateAuthLinks: (isLoggedIn) => {
                document.getElementById('auth-links').style.display = isLoggedIn ? 'none' : 'inline';
                document.getElementById('logout-link').style.display = isLoggedIn ? 'inline' : 'none';
                document.getElementById('user-profile-link').style.display = isLoggedIn ? 'inline' : 'none';
            }
        };

        // Form Utilities
        const FormUtil = {
            showMessage: (elementId, message, isError = false) => {
                const element = document.getElementById(elementId);
                element.textContent = message;
                element.className = isError ? 'error-message' : 'success-message';
                element.style.display = 'block';
                setTimeout(() => {
                    element.style.display = 'none';
                }, 5000);
            },
            clearForm: (formId) => {
                document.getElementById(formId).reset();
            }
        };

        // Initialize Application
        function initApp() {
            // Check for current user
            const currentUser = StorageUtil.getCurrentUser();
            NavUtil.updateAuthLinks(!!currentUser);
            
            // Set up navigation event listeners
            document.getElementById('home-link').addEventListener('click', (e) => {
                e.preventDefault();
                NavUtil.showSection('home-section');
            });
            
            document.getElementById('browse-quizzes-link').addEventListener('click', (e) => {
                e.preventDefault();
                loadQuizzes();
                NavUtil.showSection('browse-quizzes-section');
            });
            
            document.getElementById('user-profile-link').addEventListener('click', (e) => {
                e.preventDefault();
                if (StorageUtil.getCurrentUser()) {
                    loadUserProfile();
                    NavUtil.showSection('user-profile-section');
                } else {
                    NavUtil.showSection('login-section');
                }
            });
            
            document.getElementById('login-link').addEventListener('click', (e) => {
                e.preventDefault();
                NavUtil.showSection('login-section');
            });
            
            document.getElementById('register-link').addEventListener('click', (e) => {
                e.preventDefault();
                NavUtil.showSection('register-section');
            });
            
            document.getElementById('logout-link').addEventListener('click', (e) => {
                e.preventDefault();
                StorageUtil.logoutUser();
                NavUtil.updateAuthLinks(false);
                NavUtil.showSection('home-section');
            });
            
            // Home section buttons
            document.getElementById('create-quiz-btn').addEventListener('click', () => {
                if (StorageUtil.getCurrentUser()) {
                    setupQuizCreation();
                    NavUtil.showSection('create-quiz-section');
                } else {
                    FormUtil.showMessage('login-message', 'Please login to create a quiz', true);
                    NavUtil.showSection('login-section');
                }
            });
            
            document.getElementById('take-quiz-btn').addEventListener('click', () => {
                loadQuizzes();
                NavUtil.showSection('browse-quizzes-section');
            });
            
            // Authentication form navigation
            document.getElementById('go-to-login-btn').addEventListener('click', () => {
                NavUtil.showSection('login-section');
            });
            
            document.getElementById('go-to-register-btn').addEventListener('click', () => {
                NavUtil.showSection('register-section');
            });
            
            // Quiz creation form
            document.getElementById('cancel-create-quiz').addEventListener('click', () => {
                NavUtil.showSection('home-section');
            });
            
            // Initialize forms
            initForms();
            
            // Initialize quiz section
            document.getElementById('exit-quiz-btn').addEventListener('click', () => {
                if (confirm('Are you sure you want to exit? Your progress will be lost.')) {
                    NavUtil.showSection('browse-quizzes-section');
                }
            });
            
            document.getElementById('back-to-quizzes-btn').addEventListener('click', () => {
                loadQuizzes();
                NavUtil.showSection('browse-quizzes-section');
            });
            
            // First time setup - ensure we have storage initialized
            if (!StorageUtil.getItem('quizzes')) {
                StorageUtil.setItem('quizzes', []);
            }
            if (!StorageUtil.getItem('users')) {
                StorageUtil.setItem('users', []);
            }
            if (!StorageUtil.getItem('quizResults')) {
                StorageUtil.setItem('quizResults', []);
            }
        }

        // Initialize Forms
        function initForms() {
            // Registration Form
            document.getElementById('register-form').addEventListener('submit', (e) => {
                e.preventDefault();
                const username = document.getElementById('register-username').value;
                const email = document.getElementById('register-email').value;
                const password = document.getElementById('register-password').value;
                const confirmPassword = document.getElementById('register-confirm-password').value;
                
                if (password !== confirmPassword) {
                    FormUtil.showMessage('register-message', 'Passwords do not match!', true);
                    return;
                }
                
                const users = StorageUtil.getUsers();
                
                if (users.some(user => user.username === username)) {
                    FormUtil.showMessage('register-message', 'Username already exists!', true);
                    return;
                }
                
                if (users.some(user => user.email === email)) {
                    FormUtil.showMessage('register-message', 'Email already registered!', true);
                    return;
                }
                
                const newUser = {
                    id: Date.now(),
                    username,
                    email,
                    password, // In a real app, this would be hashed
                    quizzes: [],
                    takenQuizzes: []
                };
                
                users.push(newUser);
                StorageUtil.saveUsers(users);
                StorageUtil.setCurrentUser(newUser);
                
                FormUtil.showMessage('register-message', 'Registration successful!');
                FormUtil.clearForm('register-form');
                NavUtil.updateAuthLinks(true);
                NavUtil.showSection('home-section');
            });
            
            // Login Form
            document.getElementById('login-form').addEventListener('submit', (e) => {
                e.preventDefault();
                const username = document.getElementById('login-username').value;
                const password = document.getElementById('login-password').value;
                
                const users = StorageUtil.getUsers();
                const user = users.find(u => u.username === username && u.password === password);
                
                if (user) {
                    StorageUtil.setCurrentUser(user);
                    FormUtil.showMessage('login-message', 'Login successful!');
                    FormUtil.clearForm('login-form');
                    NavUtil.updateAuthLinks(true);
                    NavUtil.showSection('home-section');
                } else {
                    FormUtil.showMessage('login-message', 'Invalid username or password!', true);
                }
            });
            
            // Quiz Creation Form
            document.getElementById('create-quiz-form').addEventListener('submit', (e) => {
                e.preventDefault();
                saveQuiz();
            });
            
            document.getElementById('add-question-btn').addEventListener('click', () => {
                addQuestionToForm();
            });
        }

        // Quiz Creation Functions
        function setupQuizCreation() {
            const container = document.getElementById('questions-container');
            container.innerHTML = '';
            addQuestionToForm();
        }

        function addQuestionToForm() {
            const container = document.getElementById('questions-container');
            const questionIndex = container.children.length;
            
            const questionDiv = document.createElement('div');
            questionDiv.className = 'question-container';
            questionDiv.innerHTML = `
                <h4>Question ${questionIndex + 1}</h4>
                <div class="form-group">
                    <label for="question-${questionIndex}">Question:</label>
                    <input type="text" id="question-${questionIndex}" class="question-text" required>
                </div>
                <div class="options-container" id="options-container-${questionIndex}">
                    <div class="option-group">
                        <div class="form-group">
                            <label for="option-${questionIndex}-0">Option 1:</label>
                            <input type="text" id="option-${questionIndex}-0" class="option-text" required>
                        </div>
                        <input type="radio" name="correct-answer-${questionIndex}" value="0" checked> Correct
                    </div>
                    <div class="option-group">
                        <div class="form-group">
                            <label for="option-${questionIndex}-1">Option 2:</label>
                            <input type="text" id="option-${questionIndex}-1" class="option-text" required>
                        </div>
                        <input type="radio" name="correct-answer-${questionIndex}" value="1"> Correct
                    </div>
                </div>
                <button type="button" class="add-option-btn" data-question-index="${questionIndex}">Add Option</button>
                ${questionIndex > 0 ? `<button type="button" class="remove-btn" data-question-index="${questionIndex}">Remove Question</button>` : ''}
            `;
            
            container.appendChild(questionDiv);
            
            // Add event listener for adding options
            questionDiv.querySelector('.add-option-btn').addEventListener('click', function() {
                const questionIndex = this.getAttribute('data-question-index');
                addOptionToQuestion(questionIndex);
            });
            
            // Add event listener for removing questions
            const removeBtn = questionDiv.querySelector('.remove-btn');
            if (removeBtn) {
                removeBtn.addEventListener('click', function() {
                    const questionIndex = this.getAttribute('data-question-index');
                    removeQuestion(questionIndex);
                });
            }
        }

        function addOptionToQuestion(questionIndex) {
            const optionsContainer = document.getElementById(`options-container-${questionIndex}`);
            const optionIndex = optionsContainer.children.length;
            
            const optionGroup = document.createElement('div');
            optionGroup.className = 'option-group';
            optionGroup.innerHTML = `
                <div class="form-group">
                    <label for="option-${questionIndex}-${optionIndex}">Option ${optionIndex + 1}:</label>
                    <input type="text" id="option-${questionIndex}-${optionIndex}" class="option-text" required>
                </div>
                <input type="radio" name="correct-answer-${questionIndex}" value="${optionIndex}"> Correct
                ${optionIndex > 1 ? `<button type="button" class="remove-btn" data-question-index="${questionIndex}" data-option-index="${optionIndex}">Remove</button>` : ''}
            `;
            
            optionsContainer.appendChild(optionGroup);
            
            // Add event listener for removing options
            const removeBtn = optionGroup.querySelector('.remove-btn');
            if (removeBtn) {
                removeBtn.addEventListener('click', function() {
                    const qIndex = this.getAttribute('data-question-index');
                    const oIndex = this.getAttribute('data-option-index');
                    removeOption(qIndex, oIndex);
                });
            }
        }

        function removeQuestion(index) {
            const container = document.getElementById('questions-container');
            container.removeChild(container.children[index]);
            
            // Update question numbers
            for (let i = 0; i < container.children.length; i++) {
                const questionHeading = container.children[i].querySelector('h4');
                questionHeading.textContent = `Question ${i + 1}`;
            }
        }

        function removeOption(questionIndex, optionIndex) {
            const optionsContainer = document.getElementById(`options-container-${questionIndex}`);
            optionsContainer.removeChild(optionsContainer.children[optionIndex]);
            
            // Update option labels
            const options = optionsContainer.querySelectorAll('.option-group');
            for (let i = 0; i < options.length; i++) {
                const label = options[i].querySelector('label');
                label.textContent = `Option ${i + 1}:`;
                label.setAttribute('for', `option-${questionIndex}-${i}`);
                
                const input = options[i].querySelector('.option-text');
                input.id = `option-${questionIndex}-${i}`;
                
                const radio = options[i].querySelector('input[type="radio"]');
                radio.value = i;
                
                const removeBtn = options[i].querySelector('.remove-btn');
                if (removeBtn) {
                    removeBtn.setAttribute('data-option-index', i);
                }
            }
        }

        function saveQuiz() {
            const currentUser = StorageUtil.getCurrentUser();
            if (!currentUser) {
                FormUtil.showMessage('create-quiz-message', 'You must be logged in to create a quiz!', true);
                return;
            }
            
            const title = document.getElementById('quiz-title').value;
            const description = document.getElementById('quiz-description').value;
            const questions = [];
            
            const questionContainers = document.querySelectorAll('.question-container');
            for (let i = 0; i < questionContainers.length; i++) {
                const questionText = questionContainers[i].querySelector('.question-text').value;
                const optionInputs = questionContainers[i].querySelectorAll('.option-text');
                const options = Array.from(optionInputs).map(input => input.value);
                const correctAnswer = parseInt(questionContainers[i].querySelector('input[type="radio"]:checked').value);
                
                questions.push({
                    text: questionText,
                    options: options,
                    correctAnswer: correctAnswer
                });
            }
            
            const newQuiz = {
                id: Date.now(),
                title: title,
                description: description,
                questions: questions,
                creatorId: currentUser.id,
                creatorName: currentUser.username,
                createdAt: new Date().toISOString()
            };
            
            // Save quiz to storage
            const quizzes = StorageUtil.getQuizzes();
            quizzes.push(newQuiz);
            StorageUtil.saveQuizzes(quizzes);
            
            // Add quiz to user's created quizzes
            const users = StorageUtil.getUsers();
            const userIndex = users.findIndex(u => u.id === currentUser.id);
            if (userIndex !== -1) {
                if (!users[userIndex].quizzes) {
                    users[userIndex].quizzes = [];
                }
                users[userIndex].quizzes.push(newQuiz.id);
                StorageUtil.saveUsers(users);
                StorageUtil.setCurrentUser(users[userIndex]);
            }
            
            FormUtil.showMessage('create-quiz-message', 'Quiz created successfully!');
            FormUtil.clearForm('create-quiz-form');
            setTimeout(() => {
                loadQuizzes();
                NavUtil.showSection('browse-quizzes-section');
            }, 2000);
        }

        // Quiz Browsing Functions
        function loadQuizzes() {
            const quizzes = StorageUtil.getQuizzes();
            const quizList = document.getElementById('quiz-list');
            const noQuizzesMessage = document.getElementById('no-quizzes-message');
            
            quizList.innerHTML = '';
            
            if (quizzes.length === 0) {
                quizList.style.display = 'none';
                noQuizzesMessage.style.display = 'block';
                document.getElementById('create-first-quiz-btn').addEventListener('click', () => {
                    if (StorageUtil.getCurrentUser()) {
                        setupQuizCreation();
                        NavUtil.showSection('create-quiz-section');
                    } else {
                        FormUtil.showMessage('login-message', 'Please login to create a quiz', true);
                        NavUtil.showSection('login-section');
                    }
                });
            } else {
                quizList.style.display = 'block';
                noQu

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GitHub Profile Pro Flashcards</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #0d1117, #21262d);
            color: #e6edf3;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .header {
            text-align: center;
            margin-bottom: 30px;
        }

        .header h1 {
            color: #58a6ff;
            margin-bottom: 10px;
            font-size: 2.5rem;
        }

        .progress-bar {
            width: 100%;
            height: 6px;
            background: #21262d;
            border-radius: 3px;
            margin: 20px 0;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #58a6ff, #56d364);
            width: 0%;
            transition: width 0.3s ease;
            border-radius: 3px;
        }

        .stats {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        .stat {
            text-align: center;
            background: #21262d;
            padding: 15px 20px;
            border-radius: 10px;
            border: 1px solid #30363d;
        }

        .stat-number {
            font-size: 1.8rem;
            font-weight: bold;
            color: #58a6ff;
        }

        .flashcard-container {
            perspective: 1000px;
            margin: 20px 0;
        }

        .flashcard {
            width: 100%;
            height: 300px;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.6s;
            cursor: pointer;
        }

        .flashcard.flipped {
            transform: rotateY(180deg);
        }

        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            border-radius: 15px;
            padding: 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            border: 2px solid #30363d;
            background: linear-gradient(135deg, #21262d, #30363d);
        }

        .card-front {
            background: linear-gradient(135deg, #0d1117, #21262d);
            border-color: #58a6ff;
        }

        .card-back {
            transform: rotateY(180deg);
            background: linear-gradient(135deg, #1a3f2c, #238636);
            border-color: #56d364;
        }

        .card-content h3 {
            font-size: 1.4rem;
            margin-bottom: 15px;
            color: #58a6ff;
        }

        .card-back .card-content h3 {
            color: #56d364;
        }

        .card-content p {
            font-size: 1.1rem;
            line-height: 1.6;
            color: #e6edf3;
        }

        .card-content code {
            background: #161b22;
            padding: 2px 6px;
            border-radius: 4px;
            font-family: 'Courier New', monospace;
            color: #ff7b72;
            font-size: 0.9rem;
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin: 30px 0;
            flex-wrap: wrap;
        }

        .btn {
            background: #238636;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 1rem;
            transition: all 0.3s ease;
            font-weight: 500;
        }

        .btn:hover {
            background: #2ea043;
            transform: translateY(-2px);
        }

        .btn:disabled {
            background: #30363d;
            cursor: not-allowed;
            transform: none;
        }

        .btn-secondary {
            background: #21262d;
            border: 1px solid #30363d;
        }

        .btn-secondary:hover {
            background: #30363d;
        }

        .difficulty {
            text-align: center;
            margin-bottom: 20px;
        }

        .difficulty-badge {
            display: inline-block;
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: 500;
        }

        .easy { background: #238636; }
        .medium { background: #d29922; }
        .hard { background: #da3633; }

        @media (max-width: 600px) {
            .header h1 {
                font-size: 2rem;
            }
            
            .stats {
                gap: 15px;
            }
            
            .stat {
                padding: 10px 15px;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🚀 GitHub Profile Pro</h1>
            <p>Master the art of creating stunning GitHub profiles</p>
        </div>

        <div class="progress-bar">
            <div class="progress-fill" id="progressFill"></div>
        </div>

        <div class="stats">
            <div class="stat">
                <div class="stat-number" id="currentCard">1</div>
                <div>Current Card</div>
            </div>
            <div class="stat">
                <div class="stat-number" id="totalCards">20</div>
                <div>Total Cards</div>
            </div>
            <div class="stat">
                <div class="stat-number" id="completedCards">0</div>
                <div>Completed</div>
            </div>
        </div>

        <div class="difficulty">
            <span class="difficulty-badge" id="difficultyBadge">Easy</span>
        </div>

        <div class="flashcard-container">
            <div class="flashcard" id="flashcard">
                <div class="card-face card-front">
                    <div class="card-content">
                        <h3 id="questionTitle">Loading...</h3>
                        <p id="questionText">Click to start learning!</p>
                    </div>
                </div>
                <div class="card-face card-back">
                    <div class="card-content">
                        <h3>Answer</h3>
                        <p id="answerText">Answer will appear here</p>
                    </div>
                </div>
            </div>
        </div>

        <div class="controls">
            <button class="btn btn-secondary" id="prevBtn" onclick="previousCard()">← Previous</button>
            <button class="btn" id="flipBtn" onclick="flipCard()">Flip Card</button>
            <button class="btn btn-secondary" id="nextBtn" onclick="nextCard()">Next →</button>
            <button class="btn btn-secondary" onclick="shuffleCards()">🔀 Shuffle</button>
        </div>
    </div>

    <script>
        const flashcards = [
            {
                question: "What's the secret to creating animated GitHub profile headers?",
                answer: "Use SVG animations with <code>&lt;animate&gt;</code> tags, CSS keyframes in your README, or tools like GitHub Profile Header Generator. Add typing animations with libraries like Typing SVG.",
                difficulty: "easy"
            },
            {
                question: "How do you implement a dark theme for GitHub profile stats?",
                answer: "Add <code>&theme=dark</code> parameter to GitHub stats URLs like: <code>github-readme-stats.vercel.app/api?username=yourusername&theme=dark</code>",
                difficulty: "easy"
            },
            {
                question: "What are the best animated typing SVG tools for GitHub profiles?",
                answer: "Use readme-typing-svg.herokuapp.com or github-readme-typing-svg.demolab.com. Customize with parameters like speed, font, colors, and multiline text.",
                difficulty: "medium"
            },
            {
                question: "How do you create custom GitHub profile badges with animations?",
                answer: "Use shields.io with custom colors and logos, or create animated SVG badges with CSS animations. Tools like badgen.net also offer dynamic badges.",
                difficulty: "medium"
            },
            {
                question: "What's the code for adding a dynamic activity graph?",
                answer: "Use <code>github-readme-activity-graph.cyclic.app/graph?username=yourusername&theme=github-dark</code> for an animated contribution graph with dark theme.",
                difficulty: "easy"
            },
            {
                question: "How do you add interactive elements to your GitHub profile?",
                answer: "Use HTML details/summary tags for collapsible sections, embed CodePen iframes, or add click-to-reveal sections with creative markdown formatting.",
                difficulty: "hard"
            },
            {
                question: "What's the best way to showcase your tech stack with animations?",
                answer: "Use <code>skillicons.dev</code> with animation parameter: <code>https://skillicons.dev/icons?i=js,html,css,react&theme=dark&perline=8</code> or create custom SVG animations.",
                difficulty: "medium"
            },
            {
                question: "How do you create a professional GitHub profile layout structure?",
                answer: "Use HTML tables for precise alignment, center important content with <code>&lt;h1 align='center'&gt;</code>, and organize sections with clear headers and spacing.",
                difficulty: "easy"
            },
            {
                question: "What are the key elements of a standout developer profile?",
                answer: "Animated header, tech stack showcase, GitHub stats, contribution graphs, featured repositories, contact information, and a personal touch like hobbies or fun facts.",
                difficulty: "easy"
            },
            {
                question: "How do you add custom fonts and styling to GitHub README?",
                answer: "While GitHub doesn't support custom CSS, use Unicode characters, emoji styling, and SVG images with embedded fonts for custom typography effects.",
                difficulty: "hard"
            },
            {
                question: "What's the code for streak stats with dark theme?",
                answer: "<code>github-readme-streak-stats.herokuapp.com/?user=yourusername&theme=dark&hide_border=true</code> for clean dark themed streak statistics.",
                difficulty: "easy"
            },
            {
                question: "How do you create animated wave or matrix effects?",
                answer: "Use SVG with CSS animations or tools like readme-typing-svg with special characters. GitHub-profile-readme-generator offers animated templates.",
                difficulty: "hard"
            },
            {
                question: "What's the best way to highlight your best repositories?",
                answer: "Pin repositories on your profile and use <code>github-readme-stats</code> with <code>/api/pin/?username=yourusername&repo=reponame&theme=dark</code> to showcase specific projects.",
                difficulty: "medium"
            },
            {
                question: "How do you add social media links with hover effects?",
                answer: "Use SVG icons from simple-icons.org or devicon, wrap in anchor tags, and leverage GitHub's markdown image hover effects with alt text.",
                difficulty: "medium"
            },
            {
                question: "What tools help generate animated GitHub profiles automatically?",
                answer: "GitHub Profile README Generator, ProfileMe.dev, GitHub Profilinator, and Awesome GitHub Profile README templates for quick professional setups.",
                difficulty: "easy"
            },
            {
                question: "How do you create custom contribution calendar themes?",
                answer: "Use GitHub's native dark mode, or embed custom calendar widgets like grass-graph with personalized color schemes and animations.",
                difficulty: "hard"
            },
            {
                question: "What's the secret to making your profile mobile-responsive?",
                answer: "Use responsive HTML table layouts, test image sizing across devices, and ensure text remains readable. Keep animations lightweight for mobile performance.",
                difficulty: "medium"
            },
            {
                question: "How do you add a visitor counter with style?",
                answer: "Use <code>komarev.com/ghpvc/</code> with custom styling: <code>?username=yourusername&label=Profile%20views&color=0e75b6&style=flat</code> for sleek counters.",
                difficulty: "easy"
            },
            {
                question: "What are advanced markdown tricks for GitHub profiles?",
                answer: "Use HTML comments for organization, keyboard shortcuts with <code>&lt;kbd&gt;</code> tags, details/summary for FAQs, and table alignments for complex layouts.",
                difficulty: "hard"
            },
            {
                question: "How do you optimize GitHub profile loading speed?",
                answer: "Use optimized SVGs, compress images, minimize external API calls, implement lazy loading concepts, and choose lightweight animation libraries.",
                difficulty: "medium"
            }
        ];

        let currentIndex = 0;
        let isFlipped = false;
        let completedSet = new Set();

        function updateStats() {
            document.getElementById('currentCard').textContent = currentIndex + 1;
            document.getElementById('totalCards').textContent = flashcards.length;
            document.getElementById('completedCards').textContent = completedSet.size;
            
            const progress = (completedSet.size / flashcards.length) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
        }

        function updateDifficulty() {
            const difficulty = flashcards[currentIndex].difficulty;
            const badge = document.getElementById('difficultyBadge');
            badge.textContent = difficulty.charAt(0).toUpperCase() + difficulty.slice(1);
            badge.className = `difficulty-badge ${difficulty}`;
        }

        function loadCard() {
            const card = flashcards[currentIndex];
            document.getElementById('questionTitle').textContent = "💡 Pro Tip";
            document.getElementById('questionText').textContent = card.question;
            document.getElementById('answerText').innerHTML = card.answer;
            
            updateDifficulty();
            updateButtons();
            
            if (isFlipped) {
                flipCard();
            }
        }

        function flipCard() {
            const flashcard = document.getElementById('flashcard');
            flashcard.classList.toggle('flipped');
            isFlipped = !isFlipped;
            
            if (isFlipped) {
                completedSet.add(currentIndex);
                updateStats();
            }
        }

        function nextCard() {
            if (currentIndex < flashcards.length - 1) {
                currentIndex++;
                loadCard();
                updateStats();
            }
        }

        function previousCard() {
            if (currentIndex > 0) {
                currentIndex--;
                loadCard();
                updateStats();
            }
        }

        function updateButtons() {
            document.getElementById('prevBtn').disabled = currentIndex === 0;
            document.getElementById('nextBtn').disabled = currentIndex === flashcards.length - 1;
        }

        function shuffleCards() {
            for (let i = flashcards.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [flashcards[i], flashcards[j]] = [flashcards[j], flashcards[i]];
            }
            currentIndex = 0;
            completedSet.clear();
            loadCard();
            updateStats();
        }

        // Event listeners
        document.getElementById('flashcard').addEventListener('click', flipCard);

        // Keyboard navigation
        document.addEventListener('keydown', function(e) {
            if (e.key === 'ArrowLeft') previousCard();
            if (e.key === 'ArrowRight') nextCard();
            if (e.key === ' ') {
                e.preventDefault();
                flipCard();
            }
        });

        // Initialize
        loadCard();
        updateStats();
    </script>
</body>
</html>

from flask import Flask, render_template, request, redirect, url_for, session
import random
from quizzes import quizzes

app = Flask(__name__)
app.secret_key = 'temporary_secret_key'  # Secure this in production

# Welcome Page
@app.route('/', methods=['GET', 'POST'])
def index():
    if request.method == 'POST':
        username = request.form.get('username')
        session['username'] = username
        session['unlocked_topics'] = ['computer_history']  # Start with only the first topic unlocked
        session['completed_topics'] = []  # Track completed topics
        return redirect(url_for('topics'))
    return render_template('welcome.html')

# Topics Selection Page
@app.route('/topics')
def topics():
    username = session.get('username', 'Guest')
    unlocked = session.get('unlocked_topics', [])
    completed = session.get('completed_topics', [])

    # Unlock next topic only when the previous one is completed
    if "computer_history" in completed and "birth_of_programming" not in unlocked:
        unlocked.append("birth_of_programming")
    if "birth_of_programming" in completed and "birth_of_modern_programming" not in unlocked:
        unlocked.append("birth_of_modern_programming")

    # Unlock "Final Quiz" only if all 3 topics are completed
    if all(t in completed for t in ["computer_history", "birth_of_programming", "birth_of_modern_programming"]):
        if "final_quiz" not in unlocked:
            unlocked.append("final_quiz")

    session['unlocked_topics'] = unlocked  # Save updated unlocked topics
    return render_template('index.html', quizzes=quizzes, unlocked=unlocked, username=username)

# Intro Page per Topic
@app.route('/intro/<topic>')
def intro(topic):
    quiz_data = quizzes.get(topic)
    if not quiz_data or topic not in session.get('unlocked_topics', []):
        return "Topic not found or locked", 403
    return render_template('intro.html', intro=quiz_data['intro'], topic=topic)

# Quiz Page
@app.route('/quiz/<topic>')
def quiz(topic):
    quiz_data = quizzes.get(topic)
    if not quiz_data or topic not in session.get('unlocked_topics', []):
        return "Topic not found or locked", 403

    questions = quiz_data['questions']

    if topic == "final_quiz":
        if len(questions) >= 10:
            questions = random.sample(questions, 10)  # Pick 10 random questions
        session['final_quiz_questions'] = questions  # Store in session

    return render_template('quiz.html', questions=questions, topic=topic)

# Submit Route - Handles quiz submission and unlocking system
@app.route('/submit/<topic>', methods=['POST'])
def submit(topic):
    quiz_data = quizzes.get(topic)
    if not quiz_data or topic not in session.get('unlocked_topics', []):
        return "Topic not found or locked", 403

    # Retrieve the questions (Final Quiz from session)
    if topic == "final_quiz":
        questions = session.get('final_quiz_questions', [])
    else:
        questions = quiz_data['questions']

    if not questions:
        return "Error: No questions available", 500

    # Calculate Score
    score = 0
    for idx, q in enumerate(questions):
        user_answer = request.form.get(f'q{idx}')
        if user_answer == q['answer']:
            score += 1

    # Mark topic as completed if score is 3 or more
    completed = session.get('completed_topics', [])
    if score >= 3 and topic not in completed:
        completed.append(topic)

    session['completed_topics'] = completed  # Save completed topics

    return render_template('result.html', score=score, total=len(questions), topic=topic)

if __name__ == '__main__':
    app.run(debug=True)

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chatbot</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        #chatbox {
            width: 100%;
            max-width: 600px;
            margin: auto;
            background: white;
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        #messages {
            max-height: 400px;
            overflow-y: auto;
            margin-bottom: 10px;
            padding: 5px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background: #eaeaea;
        }
        .message {
            margin: 10px 0;
        }
        .user { color: blue; }
        .bot { color: green; }
        input[type="text"] {
            width: calc(100% - 22px);
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        h2 {
            text-align: center;
            color: #333;
        }
    </style>
</head>
<body>

<div id="chatbox">
    <h2>Chatbot</h2> <!-- Added chatbot name header -->
    <div id="messages"></div>
    <input type="text" id="userInput" placeholder="Type your message..." />
</div>

<script>
    const responses = {
        "hello": [
        "Hello! How can I assist you today?",
        "Hi there! What can I do for you?",
        "Greetings! How may I help you?",
        "Hey! It's great to see you here!",
        "Hello! What questions do you have for me?",
        "Hi! I'm here to help you with anything you need.",
        "Hello! I'm excited to chat with you!",
        "Hey there! How can I assist you today?",
        "Welcome! How can I help you?"
    ],
    "how are you": [
        "I'm just a computer program, but I'm here to help!",
        "Doing well, thanks! How about you?",
        "I'm here to assist you!",
        "Feeling great! What about you?",
        "I'm functioning well, thanks for asking!"
    ],
    "bye": [
        "Goodbye! Have a great day!",
        "See you later!",
        "Take care!",
        "Farewell! Until next time!",
        "Goodbye! Hope to chat again soon!",
        "It was nice talking to you! Bye!",
        "Wishing you a wonderful day ahead! Goodbye!",
        "Until next time! Stay safe!",
        "Thanks for chatting! Bye for now!",
        "See you soon! Take care!",
        "I'm glad I could help! Goodbye!",
        "Don't hesitate to return if you have more questions!",
        "Have a fantastic day! Goodbye!",
        "I hope you found our chat helpful! Bye!",
        "It was a pleasure assisting you! Goodbye!",
        "Catch you later! Have a great day!",
        "Thanks for the conversation! Farewell!",
        "I'm here whenever you need me! Bye for now!",
        "Wishing you all the best! Goodbye!",
        "Hope to chat with you again soon!",
        "Thanks for stopping by! Take care!"
    ],
    "your name": [
        "I am a chatbot created to help you!",
        "You can call me Chatbot.",
        "I'm just a friendly chatbot."
    ],
    "help": [
        "Sure! What do you need help with?",
        "I'm here to assist you. What do you want to know?",
        "How can I assist you today?"
    ],
    "staff": [
        "There are many teachers in DPS Faculty. If you want to know more about them, please visit the DPS, Yamunanagar website."
    ],
    "thank you": [
        "Happy to help.",
        "You're welcome! Let me know if you need anything else.",
        "No problem! I'm here for you."
    ],
    "stupid": [
        "No, I am not stupid, but if you are not getting any appropriate response, maybe I haven't been coded that much to give the response you need."
    ],
    "ha": [
        "Ha Ha right back at ya!"
    ],
    "principal": [
        "Mrs. Manisha Singh is the current Principal of Delhi Public School, Yamunanagar."
    ],
    "sorry": [
        "There is no need to apologize to me as I am just a chatbot."
    ],
    "best teacher": [
        "All the teachers are the best in their own field."
    ],
    "my name": [
        "I deeply apologize, but I don't know your name. However, I can help you with information about our school."
    ],
    "sports": [
        "There are many sports teachers who help students learn more about various sports and let them play the sports they like the most."
    ],
    "school hours": [
        "The school hours are from 8:00 AM to 3:00 PM from Monday to Friday."
    ],
    "subjects offered": [
        "We offer a variety of subjects including Mathematics, Science, English, History, and Geography."
    ],
    "extracurricular activities": [
        "We have various extracurricular activities such as music, dance, art, drama, and sports."
    ],
    "admission process": [
        "For admission, please visit our website for detailed information regarding eligibility and application procedures."
    ],
    "school policy": [
        "Our school policies emphasize respect, responsibility, and integrity among students and staff."
    ],
    "fees structure": [
        "The fee structure varies by grade level. Please check the school's website for the latest fee details."
    ],
    "library": [
        "Our library is open from 9 AM to 4 PM, offering a wide range of books and resources for students."
    ],
    "events": [
        "We regularly organize events such as science fairs, sports day, and cultural programs. Keep an eye on our announcements!"
    ],
    "grades": [
        "Students are graded on a scale from A to F, with A being the highest. We also have periodic assessments."
    ],
    "uniform": [
        "Students are required to wear the school uniform, which consists of a white shirt and blue trousers or skirt."
    ],
    "contact information": [
        "You can contact the school office at 123-456-7890 or email us at info@dpsyamunanagar.edu.in."
    ],
    "tuition fees": [
        "Tuition fees are collected quarterly. Please visit our website for the specific amounts for each grade."
    ],
    "school facilities": [
        "We have modern facilities including science labs, computer labs, sports fields, and a cafeteria."
    ],
    "guidance counseling": [
        "Our school provides guidance counseling to help students with academic and personal issues."
    ],
    "health services": [
        "We have a health center with a nurse available during school hours for any medical needs."
    ],
    "parent teacher meetings": [
        "Parent-teacher meetings are held twice a year to discuss student progress and concerns."
    ],
    "transportation": [
        "We offer school bus services for students in designated areas. Please check the website for routes."
    ],
    "curriculum": [
        "Our curriculum is designed to meet national standards and prepare students for higher education."
    ],
    "school calendar": [
        "The school calendar is available on our website, detailing important dates and holidays."
    ],
    "scholarships": [
        "We offer scholarships based on merit and need. Please inquire at the school office for more details."
    ],
    "after school care": [
        "After-school care is available for students until 5 PM. Contact the office for registration."
    ],
    "student council": [
        "We have an active student council that organizes events and represents student interests."
    ],
    "school committees": [
        "Various committees exist for different activities, including the cultural committee and the sports committee."
    ],
    "dress code": [
        "In addition to the uniform, there are guidelines for hairstyles and accessories that students should follow."
    ],
    "food services": [
        "Our cafeteria provides healthy meal options for students. Menu details are available weekly."
    ],
    "field trips": [
        "We organize educational field trips throughout the year to enhance learning experiences."
    ],
    "parent involvement": [
        "We encourage parents to be involved in school activities and volunteer for events."
    ],
    "tutoring services": [
        "Tutoring services are available for students needing extra help in specific subjects."
    ],
    "communication": [
        "The school communicates with parents through newsletters, emails, and the school website."
    ],
    "technology use": [
        "Students are encouraged to use technology responsibly and follow our digital citizenship guidelines."
    ],
    "art program": [
        "We have a vibrant art program where students can explore different mediums and styles."
    ],
    "music program": [
        "Our music program includes opportunities for students to learn instruments and participate in choir."
    ],
    "dance program": [
        "We offer dance classes that cover various styles, including classical and contemporary."
    ],
    "science labs": [
        "Our science labs are equipped with modern tools for conducting experiments and hands-on learning."
    ],
    "computer labs": [
        "Students have access to computer labs for research, assignments, and learning coding."
    ],
    "sports teams": [
        "We have various sports teams, including basketball, soccer, and cricket, competing at different levels."
    ],
    "coaching staff": [
        "Our coaching staff is highly experienced and dedicated to helping students excel in sports."
    ],
    "annual day": [
        "We celebrate our Annual Day with performances from students showcasing their talents."
    ],
    "workshops": [
        "We organize workshops throughout the year on various topics to enhance student skills."
    ],
    "guest speakers": [
        "We invite guest speakers to share their experiences and insights with our students."
    ],
    "safety procedures": [
        "The school has safety procedures in place, including fire drills and emergency protocols."
    ],
    "mental health support": [
        "We provide mental health resources and support for students in need."
    ],
    "community service": [
        "Students are encouraged to participate in community service projects throughout the year."
    ],
    "environmental initiatives": [
        "We promote sustainability through various environmental initiatives and programs."
    ],
    "feedback": [
        "We value feedback from students and parents to improve our school environment."
    ],
    "class schedules": [
        "Class schedules are provided at the beginning of each term and are available online."
    ],
    "orientation": [
        "New students are invited to an orientation session before the school year begins to help them adjust."
    ],
    "alumni network": [
        "Our alumni network helps former students stay connected and provides mentoring opportunities."
    ],
    "recognition programs": [
        "We have programs to recognize student achievements in academics and extracurricular activities."
    ],
    "field day": [
        "Field Day is a fun event with games and competitions, promoting teamwork and school spirit."
    ],
    "holiday breaks": [
        "The school observes several holiday breaks throughout the year, including winter and spring breaks."
    ],
    "student resources": [
        "We offer various resources for students, including study guides and online databases."
    ],
    "peer mentoring": [
        "Our peer mentoring program pairs older students with younger ones for guidance and support."
    ],
    "communication platforms": [
        "We use platforms like email and a parent portal for effective communication."
    ],
    "learning support": [
        "Additional learning support is available for students who require it through tailored programs."
    ],
    "orientation for parents": [
        "We hold orientation sessions for parents to familiarize them with school policies and procedures."
    ],
    "homework policy": [
        "Our homework policy encourages a balance between academics and personal time."
    ],
    "graduation requirements": [
        "Students must meet certain academic and attendance requirements to graduate."
    ],
    "career counseling": [
        "We provide career counseling to help students explore their future options and pathways."
    ],
    "sports events": [
        "We host various sports events throughout the year, including inter-school competitions."
    ],
    "art exhibitions": [
        "Our students' artwork is showcased in annual exhibitions, celebrating their creativity."
    ]
    };

    function normalizeInput(input) {
        return input.toLowerCase().replace(/[^\w\s]/gi, '');
    }

    function getResponse(userInput) {
        const normalizedInput = normalizeInput(userInput);
        for (const key in responses) {
            if (normalizedInput.includes(key)) {
                const responsesArray = responses[key];
                return responsesArray[Math.floor(Math.random() * responsesArray.length)];
            }
        }
        return "I'm sorry, I don't understand that. Could you please rephrase?";
    }

    document.getElementById('userInput').addEventListener('keypress', function (e) {
        if (e.key === 'Enter') {
            const userInput = this.value;
            if (userInput.toLowerCase() === 'bye') {
                addMessage("Chatbot: Goodbye! Have a great day!", "bot");
                this.value = '';
                return;
            }
            addMessage(`You: ${userInput}`, "user");
            const response = getResponse(userInput);
            addMessage(`Chatbot: ${response}`, "bot");
            this.value = '';
        }
    });

    function addMessage(message, sender) {
        const messagesDiv = document.getElementById('messages');
        const messageDiv = document.createElement('div');
        messageDiv.classList.add('message', sender);
        messageDiv.innerText = message;
        messagesDiv.appendChild(messageDiv);
        messagesDiv.scrollTop = messagesDiv.scrollHeight; // Scroll to bottom
    }
</script>

</body>
</html>

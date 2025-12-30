# Ask Lagronian - Lagro High School Chatbot

An intelligent chatbot assistant for Lagro High School's Senior High School program, powered by Google's Gemini AI. This chatbot provides accurate, relevant information to current and prospective students and their parents/guardians.

## Features

### Public Features (No Login Required)
- **Homepage**: Informative landing page with school information
- **Programs Overview**: Details about STEM, HUMSS, ABM, and TVL tracks
- **Contact Information**: Easy access to school contact details and social media
- **Responsive Design**: Works seamlessly on desktop and mobile devices

### Protected Features (Login Required)
- **Google OAuth Authentication**: Secure sign-in with Google accounts
- **AI-Powered Chatbot**: Access to Ask Lagronian AI assistant
- **Conversation History**: Session-based chat history for contextual responses
- **PDF Knowledge Base**: AI trained on comprehensive school information
- **Real-time Responses**: Instant answers with timestamps
- **User Profile**: Personalized experience with user information
- **Comprehensive Coverage**: Information about:
  - Academic tracks and strands (STEM, HUMSS, ABM, TVL)
  - Enrollment procedures
  - Curriculum and subjects
  - School facilities and services
  - Rules and regulations
  - Extracurricular activities

## Tech Stack

- **Backend**: Flask (Python)
- **Authentication**: Google OAuth 2.0 (Authlib)
- **AI Model**: Google Gemini 2.0 Flash
- **Frontend**: HTML, CSS, JavaScript
- **Deployment**: Vercel-ready configuration

## Installation

### Prerequisites

- Python 3.8 or higher
- pip (Python package installer)
- Google Gemini API key
- Google Cloud Project (for OAuth credentials)

### Setup Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/asklagronian.git
   cd asklagronian
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv

   # On Windows
   venv\Scripts\activate

   # On macOS/Linux
   source venv/bin/activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up Google OAuth Credentials**
   - Go to [Google Cloud Console](https://console.cloud.google.com/)
   - Create a new project or select an existing one
   - Enable the Google+ API
   - Go to "Credentials" → "Create Credentials" → "OAuth 2.0 Client ID"
   - Choose "Web application"
   - Add authorized redirect URI: `http://localhost:5000/authorize` (for local development)
   - Save the Client ID and Client Secret

5. **Set up environment variables**
   - Copy `.env.example` to `.env`
   ```bash
   cp .env.example .env
   ```
   - Edit `.env` and add your credentials:
   ```
   GEMINI_API_KEY=your_gemini_api_key_here
   SECRET_KEY=your_secret_key_here (generate a random string)
   GOOGLE_CLIENT_ID=your_google_client_id
   GOOGLE_CLIENT_SECRET=your_google_client_secret
   ```

   - Get Gemini API key from: https://makersuite.google.com/app/apikey
   - Get OAuth credentials from: https://console.cloud.google.com/apis/credentials

6. **Run the application**
   ```bash
   python app.py
   ```

7. **Open your browser**
   - Navigate to `http://localhost:5000` for the homepage
   - Click "Sign In" to login with Google
   - After authentication, you'll be redirected to the chatbot

## Project Structure

```
asklagronian/
├── app.py                          # Main Flask application
├── requirements.txt                # Python dependencies
├── .env.example                    # Environment variables template
├── .gitignore                      # Git ignore rules
├── vercel.json                     # Vercel deployment config
├── wsgi.py                         # WSGI entry point
├── Lagro High School - Data.pdf    # School information PDF (local only, not in repo)
├── static/
│   ├── css/
│   │   ├── style.css              # Chatbot page styling
│   │   └── home.css               # Homepage styling
│   ├── js/
│   │   ├── script.js              # Chatbot JavaScript
│   │   └── home.js                # Homepage JavaScript
│   └── images/                     # Image assets
└── templates/
    ├── home.html                   # Public homepage
    └── chatbot.html                # Protected chatbot page
```

## Configuration

### Environment Variables

- `GEMINI_API_KEY`: Your Google Gemini API key (required)
- `SECRET_KEY`: Flask secret key for session management (required)
- `GOOGLE_CLIENT_ID`: Google OAuth Client ID (required)
- `GOOGLE_CLIENT_SECRET`: Google OAuth Client Secret (required)

### PDF Knowledge Base

Place your school information PDF file in the root directory and update the path in `app.py`:

```python
PDF_FILE_PATH = 'Lagro High School - Data .pdf'
```

## API Endpoints

### Public Routes
- `GET /` - Homepage (public, no login required)

### Authentication Routes
- `GET /login` - Initiate Google OAuth login
- `GET /authorize` - OAuth callback handler
- `GET /logout` - Logout and clear session

### Protected Routes (Require Login)
- `GET /chatbot` - Chatbot interface (login required)
- `POST /send_message` - Send a message and get AI response
- `POST /clear_history` - Clear conversation history for current session

## Deployment

### Deploy to Vercel

1. Install Vercel CLI:
   ```bash
   npm install -g vercel
   ```

2. Deploy:
   ```bash
   vercel
   ```

3. Set environment variables in Vercel dashboard:
   - `GEMINI_API_KEY`
   - `SECRET_KEY`
   - `GOOGLE_CLIENT_ID`
   - `GOOGLE_CLIENT_SECRET`

4. Update OAuth redirect URI in Google Cloud Console:
   - Add your Vercel domain: `https://your-app.vercel.app/authorize`

### Deploy to Other Platforms

The application is a standard Flask app and can be deployed to:
- Heroku
- Railway
- PythonAnywhere
- AWS/GCP/Azure

Make sure to set the environment variables on your deployment platform.

## Features Implemented

### Conversation Management
- Session-based conversation history
- Context-aware responses
- Automatic history cleanup (keeps last 20 exchanges)

### Security
- Environment variable protection
- Input validation and sanitization
- Message length limits (2000 characters)
- Error handling and logging

### Logging
- Application logs stored in `app.log`
- Session tracking
- Error tracking with stack traces

## Improvements Made

This improved version includes:

1. **Google OAuth Authentication**: Secure login with Google accounts
2. **Public Homepage**: Informative landing page with school information
3. **Protected Chatbot**: Chatbot accessible only after authentication
4. **Session Management**: Maintains conversation context across messages
5. **Error Handling**: Comprehensive error handling with proper logging
6. **Input Validation**: Validates and sanitizes user input
7. **Security**: Protected API keys, OAuth security, proper .gitignore
8. **Functional Navigation**: Working menu with clickable links
9. **User Profiles**: Display logged-in user information
10. **Logging**: Detailed logging for debugging and monitoring
11. **Modern Design**: Educational website with responsive layout
12. **Documentation**: Complete setup instructions and API documentation

## Usage Tips

1. **First Message**: The chatbot will ask for your name to personalize the experience
2. **Clear Conversations**: Use the refresh button to start a new conversation
3. **Specific Questions**: Ask specific questions about enrollment, courses, or school services
4. **Language Support**: The chatbot supports both English and Filipino

## Troubleshooting

### Common Issues

1. **"GEMINI_API_KEY not found" error**
   - Make sure you've created a `.env` file with your API key
   - Verify the API key is valid

2. **PDF file not found**
   - Ensure the PDF file path in `app.py` is correct
   - Check that the PDF file exists in the specified location

3. **Port already in use**
   - Change the port in `app.py`:
   ```python
   app.run(debug=True, port=5001)
   ```

## Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit your changes: `git commit -am 'Add new feature'`
4. Push to the branch: `git push origin feature-name`
5. Submit a pull request

## Credits

- **Developer**: Lanz Colico (Former Lagro High School student)
- **School**: Lagro High School, Quezon City
- **AI Model**: Google Gemini 2.0 Flash

## License

This project is created for Lagro High School's educational purposes.

## Contact

For issues, questions, or contributions:
- School Email: hs.lagro@depedqc.ph
- School Phone: 8939 1092
- GitHub Issues: [Create an issue](https://github.com/yourusername/asklagronian/issues)

## Acknowledgments

- Lagro High School administration and faculty
- Google for the Gemini AI platform
- All contributors and testers

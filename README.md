# Ask Lagronian - Lagro High School Chatbot

An intelligent chatbot assistant for Lagro High School's Senior High School program, powered by Google's Gemini AI. This chatbot provides accurate, relevant information to current and prospective students and their parents/guardians.

## Features

- **AI-Powered Responses**: Utilizes Google's Gemini 2.0 Flash model for intelligent, context-aware responses
- **PDF Knowledge Base**: Integrates school information from PDF documents for accurate answers
- **Conversation History**: Maintains session-based conversation history for contextual responses
- **Modern UI**: Clean, responsive interface with dark/light theme support
- **Real-time Chat**: Instant responses with message timestamps
- **Comprehensive Coverage**: Information about:
  - Academic tracks and strands (STEM, HUMSS, ABM, TVL)
  - Enrollment procedures
  - Curriculum and subjects
  - School facilities and services
  - Rules and regulations
  - Extracurricular activities

## Tech Stack

- **Backend**: Flask (Python)
- **AI Model**: Google Gemini 2.0 Flash
- **Frontend**: HTML, CSS, JavaScript
- **Deployment**: Vercel-ready configuration

## Installation

### Prerequisites

- Python 3.8 or higher
- pip (Python package installer)
- Google Gemini API key

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

4. **Set up environment variables**
   - Copy `.env.example` to `.env`
   ```bash
   cp .env.example .env
   ```
   - Edit `.env` and add your Google Gemini API key:
   ```
   GEMINI_API_KEY=your_actual_api_key_here
   SECRET_KEY=your_secret_key_here
   ```

   Get your Gemini API key from: https://makersuite.google.com/app/apikey

5. **Run the application**
   ```bash
   python app.py
   ```

6. **Open your browser**
   Navigate to `http://localhost:5000`

## Project Structure

```
asklagronian/
├── app.py                          # Main Flask application
├── requirements.txt                # Python dependencies
├── .env.example                    # Environment variables template
├── .gitignore                      # Git ignore rules
├── vercel.json                     # Vercel deployment config
├── wsgi.py                         # WSGI entry point
├── Lagro High School - Data.pdf    # School information PDF
├── static/
│   ├── css/
│   │   └── style.css              # Styling
│   ├── js/
│   │   └── script.js              # Frontend JavaScript
│   └── images/                     # Image assets
└── templates/
    └── index.html                  # Main HTML template
```

## Configuration

### Environment Variables

- `GEMINI_API_KEY`: Your Google Gemini API key (required)
- `SECRET_KEY`: Flask secret key for session management (auto-generated if not provided)

### PDF Knowledge Base

Place your school information PDF file in the root directory and update the path in `app.py`:

```python
PDF_FILE_PATH = 'Lagro High School - Data .pdf'
```

## API Endpoints

- `GET /` - Main chatbot interface
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

1. **Session Management**: Maintains conversation context across messages
2. **Error Handling**: Comprehensive error handling with proper logging
3. **Input Validation**: Validates and sanitizes user input
4. **Security**: Protected API keys, proper .gitignore configuration
5. **Logging**: Detailed logging for debugging and monitoring
6. **Documentation**: Complete README and code comments
7. **Code Organization**: Better structured and more maintainable code

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

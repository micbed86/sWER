# sWER - Semantic Word Error Rater

An advanced web-based tool to calculate, visualize, and semantically analyze transcription errors, going beyond standard metrics by leveraging AI to understand the _meaning_ behind mistakes.

## About The Project

Standard transcription quality metrics like Word Error Rate (WER) and Character Error Rate (CER) are invaluable, but they treat all errors equally. A simple typo like "the" vs. "teh" is counted the same as a critical semantic error like "approve" vs. "oppose".

**WERer** was built to bridge that gap. It not only provides standard metrics but also introduces **Semantic Word Error Rate (S-WER)**, a concept powered by Google's Gemini AI. The tool visually highlights differences and allows the AI to determine whether an error is merely formal (e.g., punctuation, regional spelling) or semantic (i.e., it changes the meaning of the sentence).

This makes it an essential tool for:

*   Developers working on Automatic Speech Recognition (ASR) models.
    
*   Quality assurance teams verifying transcription accuracy.
    
*   Researchers analyzing linguistic data and transcription fidelity.
    
*   Anyone needing a deeper, more nuanced understanding of text differences.
    

## Key Features

*   **Standard Metrics:** Calculates Word Error Rate (WER) and Character Error Rate (CER).
    
*   **AI-Powered Semantic Analysis:** Uses the Google Gemini API to intelligently classify errors as "semantic" or "formal," providing a Semantic WER.
    
*   **Interactive Side-by-Side Diff:** Visually inspects substitutions, insertions, and deletions in a clear, color-coded interface.
    
*   **Full Interactivity:**
    
    *   **Re-classify Errors:** Right-click any error to manually change its type (e.g., change a substitution to a formal error).
        
    *   **Inline Editing:** Correct mistakes directly in the diff view.
        
    *   **Ignore Errors:** Temporarily exclude errors from metric calculations.
        
*   **Smart Text Normalization:** Optional feature to ignore case, punctuation, and formatting for a content-focused comparison.
    
*   **Secure API Key Handling:** Your Google AI API key is stored securely in your browser's `sessionStorage` or `localStorage` and is never exposed or sent to any server other than Google's.
    
*   **Responsive Design:** Fully functional on both desktop and mobile devices.
    
*   **No Backend Needed:** A completely self-contained, single-file HTML application.
    

## How It Works

The application's logic is built on three pillars:

1.  **Levenshtein Distance:** The core comparison is powered by the Levenshtein algorithm. This classic dynamic programming approach calculates the minimum number of single-character edits (insertions, deletions, or substitutions) required to change one word into the other. This is used for both word-level alignment (for WER) and character-level alignment (for CER).
    
2.  **Centralized State Management:** All comparison data, including word pairs, error types, and user modifications, is held in a single JavaScript state object (`comparisonState`). The entire UI—from the metric cards to the interactive diff views—is a direct rendering of this state. When a user edits a word or re-classifies an error, the state is updated, and the UI automatically re-renders to reflect the change.
    
3.  **AI-Driven Contextual Analysis:** This is the tool's most powerful feature.
    
    *   **Chunking:** Instead of analyzing single-word errors in isolation, the app groups consecutive errors into "chunks."
        
    *   **Contextualization:** It then grabs surrounding correct words (the context) for each chunk.
        
    *   **Prompt Engineering:** A carefully crafted system prompt is sent to the Google Gemini API, along with the error chunk and its context. The prompt instructs the model to act as a transcription expert and return a simple `true` or `false` decision on whether the error is semantic, using a strict JSON schema for a reliable response.
        

## Getting Started

As a single-file application, there is no installation or build process required.

1.  Download the `index.html` file from this repository.
    
2.  Open the file in any modern web browser (like Chrome, Firefox, or Edge).
    

### Usage

1.  **Paste Text:** Paste your reference text into the "Source (Ground Truth)" box and the transcribed text into the "Hypothesis (Transcription)" box.
    
2.  **Compare:** Click the **Compare** button.
    
3.  **Review Results:** The metric cards will populate with WER, CER, and counts for substitutions, deletions, and insertions. The diff panels below will show a detailed, color-coded breakdown.
    
4.  **Interact (Optional):**
    
    *   Right-click on any highlighted word in the diff view to open a context menu.
        
    *   From here, you can re-classify the error type, ignore it, or edit the word directly. Your changes will instantly update all metrics.
        

### Semantic Analysis (AI)

To use the AI-powered semantic analysis:

1.  Click the **Semantic Analysis (AI)** button.
    
2.  If you haven't provided an API key before, a modal will appear.
    
3.  **Get a Key:** Obtain a free Google AI API key from [Google AI Studio](https://aistudio.google.com/app/apikey "null").
    
4.  **Enter and Save:** Paste the key into the modal. You can choose to remember it for the current session or permanently on your device (using `localStorage`).
    
5.  The tool will then send all relevant errors to the Gemini API for analysis. When it's done, the **Semantic WER** will be calculated, and formal errors will be visually styled differently in the diff view.
    

## Technology Stack

*   **HTML5:** For the application structure.
    
*   **CSS3:** For the custom "Neon UI" styling, utilizing Flexbox, Grid, Custom Properties, and Keyframe Animations.
    
*   **Vanilla JavaScript (ES6+):** For all application logic, including the Levenshtein algorithm, state management, and DOM manipulation. No external libraries or frameworks are used.
    
*   **Google Gemini API:** The generative AI model used for semantic error classification.
    

## Contributing

Contributions are what make the open-source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".

1.  Fork the Project
    
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
    
3.  Commit your Changes (`git commit -m 'feat(ui): add amazing feature'`)
    
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
    
5.  Open a Pull Request
    

Please adhere to the **Conventional Commits** specification for commit messages.

## License

Distributed under the MIT License. See the `LICENSE` file in the repository for more information.

## Acknowledgments

*   The visual theme is inspired by the "Neon UI Style by micbed86".
    
*   This project relies on the powerful capabilities of the Google Gemini model.
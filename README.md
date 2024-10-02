Due to the european portuguese variant is rare to found and hard to translate, my project is to translate many types of files into PT-PT.

This code facilitates the translation of subtitles from an English `.srt` file into European Portuguese using the GPT-4 API, while managing file selection, text processing, and progress tracking. Here's a breakdown of each part:

### Libraries:
- **os**: Handles environment variables and file paths.
- **re**: For regular expressions, used in parsing the SRT file.
- **openai**: Interacts with the OpenAI API for translation.
- **tqdm.auto**: Displays progress bars for tasks.
- **dotenv**: Loads environment variables from a `.env` file.
- **tkinter**: Provides a GUI dialog for selecting files.
- **termcolor**: Adds colored text to terminal output.
- **IPython.display**: Displays formatted HTML in Jupyter for visual output.

### Function Breakdown:

1. **load_dotenv()**:
   - Loads environment variables from a `.env` file. The OpenAI API key is expected to be stored in this file.
   
2. **Retrieve and set OpenAI API Key**:
   - Retrieves the `OPENAI_API_KEY` from environment variables. If it's not found, the program raises an error to avoid proceeding without the necessary API credentials.

3. **translate_text()**:
   - Translates a given block of text from the source language (`en`) to the target language (`pt-PT`) using GPT-4-turbo. The OpenAI API is called with a `system` role that defines the task (translation) and a `user` role for the actual text content.
   - Extracts and returns the translated text from the API response.

4. **parse_srt()**:
   - Reads an SRT (subtitle) file and splits the content into sections using regular expressions. Each section corresponds to a subtitle entry with an index, timestamp, and text.
   - Returns a list of tuples in the format `(index, timestamp, text)` for easy manipulation.

5. **write_srt()**:
   - Writes the translated subtitles back to a new SRT file, preserving the original formatting (index, timestamp, and translated text).

6. **display_translations()**:
   - Displays the original and translated subtitles side by side in HTML, formatted with blue for original text and green for translated text. This is useful for comparison or debugging, especially in Jupyter environments.

7. **main()**:
   - The core logic of the program:
     - Reads the selected subtitle file.
     - Parses it using `parse_srt()`.
     - Translates the content subtitle by subtitle, using a progress bar to indicate translation progress.
     - Displays both original and translated text side by side using HTML.
     - Writes the translated content into a new SRT file using `write_srt()`.
   
8. **Tkinter-based file selection**:
   - A graphical file dialog is opened to allow the user to select the English `.srt` file for translation. This ensures ease of use, as the user doesn't need to manually provide a file path.

9. **Program Execution**:
   - The program starts by hiding the root Tkinter window and then opens the file dialog for subtitle selection. If a file is selected, the `main()` function is invoked to perform the translation. If no file is selected, the program exits.

### Workflow:
1. The user selects an `.srt` file using a dialog window.
2. The program parses the file and translates the subtitles line-by-line using the OpenAI GPT-4 API.
3. Both the original and translated subtitles are displayed for visual comparison.
4. The translated subtitles are saved to a new file, appending `_PT-PT` to the filename.

This setup ensures that users can easily translate their subtitle files with minimal interaction and clear feedback throughout the process.

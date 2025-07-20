# LinkedIn Icebreaker & Chat Bot

A conversational AI assistant built with LlamaIndex and Gradio that generates personalized icebreakers for LinkedIn profiles and allows for follow-up questions.

## Features

* **Personalized Icebreakers:** Generates unique conversation starters based on a LinkedIn profile's professional background, roles, companies, and education.
* **Conversational Chat:** Engage in a back-and-forth dialogue with the AI about the scraped LinkedIn profile.
* **Bright Data Integration:** Fetches real-time public LinkedIn profile data using Bright Data's Web Scraper API.
* **LlamaIndex RAG:** Leverages Retrieval Augmented Generation (RAG) with an in-memory ChromaDB vector store to ground responses in profile data.
* **Gradio Interface:** Provides an easy-to-use web interface for interaction.

## How It Works

1.  **Data Acquisition:** The bot uses the [Bright Data Web Scraper API](https://brightdata.com/) to fetch public LinkedIn profile information.
2.  **Document Creation:** The raw profile data is converted into a structured LlamaIndex `Document`.
3.  **Chunking & Embedding:** The document is split into smaller chunks (nodes), and these nodes are converted into numerical embeddings using a HuggingFace Sentence Transformer model.
4.  **Vector Storage:** These embeddings are stored in an in-memory [ChromaDB](https://www.trychroma.com/) vector store.
5.  **Retrieval Augmented Generation (RAG):**
    * When an icebreaker is requested or a question is asked in chat, the system retrieves the most relevant chunks from the profile based on the query.
    * These retrieved chunks are then provided as context to a Large Language Model (LLM - OpenAI's GPT-3.5-turbo in this case).
    * The LLM generates a personalized response grounded in the profile data.
6.  **Gradio Interface:** A web-based UI built with Gradio allows users to input LinkedIn URLs and interact with the bot.

## Setup and Running (Google Colab)

This project is designed to run seamlessly in Google Colab.

1.  **Open the Notebook:** Click on the `LinkedIn_Icebreaker_Bot.ipynb` (or your chosen name) file in this GitHub repository. You will see a button "Open in Colab". Click it.
2.  **Set up API Keys:**
    * You need an **OpenAI API Key** and a **Bright Data API Key**.
    * In Colab, go to **`Secrets`** (on the left sidebar, looks like a key icon).
    * Add two new secrets:
        * `OPENAI_API_KEY` (paste your OpenAI API key here)
        * `BRIGHTDATA_API_KEY` (paste your Bright Data API key here)
    * Ensure "Notebook access" is toggled ON for both secrets.
3.  **Run All Cells:** Go to **`Runtime`** > **`Run all`**.
4.  **Launch Gradio Interface:** After all cells have executed, the last cell will output a public Gradio URL (e.g., `https://xxxx.gradio.live`). Click this link to open the web interface.
5.  **Interact:** Enter a public LinkedIn profile URL in the provided textbox and click "Generate Icebreaker". Once the icebreaker appears, a chat interface will become visible for follow-up questions.

## Important Notes

* **Bright Data Credits:** Fetching real LinkedIn profile data consumes Bright Data credits. For testing without consuming credits, set `USE_MOCK_DATA_FOR_TEST = True` in Cell 5.
* **Public Profiles Only:** The Bright Data scraper can only access publicly available LinkedIn profile information.
* **In-Memory Database:** The ChromaDB vector store is in-memory, meaning the indexed profile data is cleared with each new request in the Gradio app.

## Contributing

Feel free to fork this repository, open issues, or submit pull requests.

## License

[Specify your license, e.g., MIT License - see LICENSE file for details]

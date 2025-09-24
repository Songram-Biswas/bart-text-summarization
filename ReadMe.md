# **Text Summarization with BART**

This project demonstrates how to fine-tune a pre-trained **BART (Bidirectional and Auto-Regressive Transformers)** model from Hugging Face for the task of abstractive text summarization. The model is fine-tuned on a subset of the popular **CNN/DailyMail** dataset, a standard benchmark for this task.

## **Features**

* **Fine-tuning**: Adapts a pre-trained bart-base model for the specific task of summarization.  
* **Dataset Integration**: Uses the datasets library to easily load and preprocess the CNN/DailyMail dataset.  
* **Efficient Training**: Leverages the Hugging Face Trainer API for a streamlined training loop with built-in features like mixed-precision training (fp16).  
* **Real-time Generation**: Includes a demo section to generate a new summary from a test article, showcasing the model's performance after fine-tuning.

## **Prerequisites**

To run this script, you will need to install the following Python libraries. You can do so by running this command in your terminal:

pip install transformers datasets accelerate

## **Usage**

1. **Save the Code**: Save the provided Python script as fine\_tune\_bart.py.  
2. **Run the Script**: Execute the file from your terminal. The script will automatically handle data loading, preprocessing, fine-tuning, and a test run.

python fine\_tune\_bart.py

The training process will take some time, depending on your hardware (a GPU is highly recommended). The script is configured to train for only one epoch on a small subset of the data (1000 examples) for demonstration purposes.

## **Code Walkthrough**

The script is divided into the following key sections:

* **Data Loading**: The load\_dataset function fetches the CNN/DailyMail data.  
* **Model and Tokenizer**: The AutoTokenizer and AutoModelForSeq2SeqLM classes are used to load the pre-trained bart-base checkpoint.  
* **Preprocessing**: The preprocess\_function handles the tokenization of both the input articles and the target summaries, preparing the data for the model.  
* **Training**: The TrainingArguments class configures the training process, and the Trainer class executes the fine-tuning loop. The DataCollatorForSeq2Seq is crucial for correctly padding the input and output sequences.  
* **Inference**: After training, the model.generate() method is used with beam search to create a high-quality summary from a new article.

## **Example Output**

After running the script, you will see output similar to the following, demonstrating the model's generated summary against the reference summary from the dataset.

\--- Starting Fine-Tuning \---

... (training logs) ...

\--- Generated Summary \---

Article (First 400 chars): (CNN)The Palestinian Authority officially became the 123rd member of the International Criminal Court on Wednesday, a step that gives the court jurisdiction over alleged crimes in Palestinian territories. The formal accession was marked with a ceremony at The Hague, in the Netherlands, where the court is based. The Palestinians signed the ICC's founding Rome Statute in January, when they also acce

Reference Summary: Membership gives the ICC jurisdiction over alleged crimes committed in Palestinian territories since last June .  
Israel and the United States opposed the move, which could open the door to war crimes investigations against Israelis .

Generated Summary: The Palestinian Authority officially became the 123rd member of the International Criminal Court. The formal accession was marked with a ceremony at The Hague. The move was opposed by Israel and the United States.

## **Acknowledgments**

* **Hugging Face**: For providing the transformers library and pre-trained models.  
* **Google Research**: For providing the CNN/DailyMail dataset.
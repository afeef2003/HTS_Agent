# HTS_Agent_Task (no api key required)- Syeda Shamama Afeef

# HTS AI Agent - Free Version 🤖  (colab notebook link:- https://colab.research.google.com/drive/1wWAqNijjV8c7ZVWwBW4j00eLallm7JEO?usp=sharing )

A free, no-cost AI agent for Harmonized Tariff Schedule (HTS) classification, duty calculations, and trade policy assistance. No OpenAI API key required!

## 🌟 Features

- **Tariff Calculations**: Calculate duties for any HTS code with cost, freight, and insurance
- **Trade Policy Q&A**: Get answers about FTAs, GSP, NAFTA, and trade agreements
- **HTS Code Search**: Find HTS codes by product description
- **Interactive Chat**: Natural language interface for all queries
- **100% Free**: Uses open-source models - no API costs

## 🚀 Quick Start

### Prerequisites

- Python 3.7+
- Google Colab (recommended) or local Jupyter environment

### Installation

1. **Clone or download the project files**
2. **Open in Google Colab** (recommended for free GPU access)
3. **Run cells in order** - the system will auto-install all dependencies

```python
# Cell 1: Install packages (runs automatically)
!pip install langchain langchain-community chromadb pandas numpy
!pip install sentence-transformers faiss-cpu transformers torch
!pip install huggingface-hub accelerate
```

### Basic Usage

```python
# After running all setup cells, use the bot:
response = free_bot.chat("What is the United States-Israel Free Trade Agreement?")
print(response)

# Calculate duties
response = free_bot.chat("Given HTS code 0101.30.00.00, cost $10000, freight $500, insurance $100")
print(response)

# Search HTS codes
response = free_bot.chat("What's the HTS code for donkeys?")
print(response)
```

## 📊 Sample Data

The system includes sample HTS data for testing:

| HTS Number    | Description         | General Rate | Special Rate |
| ------------- | ------------------- | ------------ | ------------ |
| 0101.30.00.00 | Asses (donkeys)     | Free         | Free         |
| 0201.10.00.00 | Beef, fresh/chilled | 26.4¢/kg    | Free (FTA)   |
| 0401.10.00.00 | Milk and cream      | 3.2¢/liter  | Free (FTA)   |
| 1001.11.00.00 | Durum wheat seed    | 5.7¢/kg     | Free (FTA)   |
| 2203.00.00.00 | Beer made from malt | $0.233/liter | Free (FTA)   |

## 💬 Example Queries

### Trade Policy Questions

```
"What is the United States-Israel Free Trade Agreement?"
"Can a product that exceeds its tariff-rate quota still qualify for duty-free entry under GSP?"
"How is classification determined for an imported item?"
```

### Tariff Calculations

```
"Given HTS code 0101.30.00.00, cost $10000, freight $500, insurance $100"
"Calculate duties for HTS 0201.10.00.00 with cost $5000, 100 kg weight"
"What are the duties for HTS 2203.00.00.00, cost $2000, 500 liters?"
```

### HTS Code Searches

```
"What's the HTS code for donkeys?"
"Find HTS codes for beef products"
"What codes are available for dairy products?"
```

## 🔧 System Architecture

### Core Components

1. **FreeAIModels**: Manages open-source AI models

   - Sentence transformers for embeddings
   - Rule-based Q&A system
   - Text generation pipeline
2. **FreeRAGSystem**: Knowledge base search

   - Trade agreement information
   - Classification rules
   - Policy explanations
3. **FreeTariffCalculator**: Duty calculations

   - Supports percentage duties (e.g., "5%")
   - Weight-based duties (e.g., "26.4¢/kg")
   - Volume-based duties (e.g., "$0.233/liter")
   - CIF value calculations
4. **FreeTariffBot**: Main chat interface

   - Query classification
   - Response routing
   - Natural language processing

### Data Flow

```
User Query → Query Classification → Route to Handler → Generate Response
                    ↓
    Policy Questions → RAG System → Knowledge Base Search
    Calculations → Tariff Calculator → Duty Computation
    Searches → HTS Database → Code Lookup
```

## 📋 Installation Guide

### Option 1: Google Colab (Recommended)

1. Open [Google Colab](https://colab.research.google.com/)
2. Create new notebook
3. Copy and run cells from the provided code
4. All dependencies install automatically

### Option 2: Local Installation

```bash
# Create virtual environment
python -m venv hts_env
source hts_env/bin/activate  # Linux/Mac
# or
hts_env\Scripts\activate  # Windows

# Install dependencies
pip install langchain langchain-community
pip install chromadb pandas numpy
pip install sentence-transformers faiss-cpu
pip install transformers torch
pip install huggingface-hub accelerate
```

## 🧪 Testing

Run the built-in test suite:

```python
# Tests all core functionality
test_questions = [
    "What is the United States-Israel Free Trade Agreement?",
    "Can a product that exceeds its tariff-rate quota still qualify for duty-free entry?",
    "How is classification determined for an imported item?",
    "Given HTS code 0101.30.00.00, cost $10000, freight $500, insurance $100",
    "What's the HTS code for donkeys?",
    "What are the applicable duty rates for beef?"
]

for question in test_questions:
    response = free_bot.chat(question)
    print(f"Q: {question}")
    print(f"A: {response}\n")
```

## 🔍 Advanced Features

### Custom HTS Data

Replace `hts_data.csv` with your own data:

```python
# Load custom HTS data
custom_data = pd.read_csv("your_hts_data.csv")
tariff_calc = FreeTariffCalculator("your_hts_data.csv")
```

### Extended Knowledge Base

Add more trade policies:

```python
free_rag.knowledge_base["New Agreement"] = """
Your trade agreement information here...
"""
```

### Batch Processing

Process multiple calculations:

```python
hts_codes = ["0101.30.00.00", "0201.10.00.00", "0401.10.00.00"]
for code in hts_codes:
    result = tariff_calc.calculate_duties(code, 10000, 500, 100)
    print(tariff_calc.format_calculation_result(result))
```

## 🚨 Troubleshooting

### Common Issues

**Model Loading Errors**

```python
# If models fail to load, try:
import torch
torch.cuda.empty_cache()  # Clear GPU memory

# Or use CPU-only mode:
device = "cpu"
```

**Memory Issues**

```python
# Reduce model size for limited memory:
embeddings_model = SentenceTransformer('all-MiniLM-L6-v2')  # Smaller model
```

**Import Errors**

```bash
# Update packages:
pip install --upgrade transformers sentence-transformers
```

## 📈 Performance Optimization

### For Large Datasets

- Use FAISS indexing for faster searches
- Implement chunking for large documents
- Cache embeddings to reduce computation

### For Production Use

- Add input validation
- Implement error handling
- Use async processing for multiple queries
- Add logging and monitoring

## 🔒 Security Notes

- No API keys required - completely offline after model download
- No external API calls during runtime
- All processing happens locally
- Safe for sensitive trade data

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature-name`
3. Commit changes: `git commit -am 'Add feature'`
4. Push to branch: `git push origin feature-name`
5. Submit pull request

### Areas for Contribution

- Additional trade agreement knowledge
- More HTS classification data
- Enhanced duty calculation logic
- UI/UX improvements
- Performance optimizations

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- **Hugging Face** for open-source transformers
- **Sentence Transformers** for embedding models
- **LangChain** for RAG framework
- **U.S. Trade Representative** for HTS data

## 📞 Support

For questions and support:

- Create an issue in the repository
- Check the troubleshooting section
- Review example queries for proper format

## 🔄 Version History

- **v1.0.0** - Initial release with core functionality
- **v1.1.0** - Added interactive chat interface
- **v1.2.0** - Enhanced duty calculation logic

---

**Made with ❤️ By Syeda Shamama Afeef

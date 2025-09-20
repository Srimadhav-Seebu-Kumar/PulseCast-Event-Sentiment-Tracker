# PulseCast: Event Sentiment Tracker

## Overview

PulseCast is a real-time sentiment analysis and event tracking system designed to monitor public opinion and emerging trends across social media platforms and news sources. The system provides comprehensive insights into public sentiment around specific events, topics, or entities through advanced natural language processing and machine learning techniques.

## Key Features

### Real-Time Data Processing
- **Multi-Source Data Ingestion**: Collects data from Twitter, Reddit, news APIs, and other social media platforms
- **Stream Processing**: Real-time data processing using Apache Kafka and Apache Spark
- **Event Detection**: Automatically identifies trending topics and breaking events

### Sentiment Analysis
- **Advanced NLP Models**: Utilizes transformer-based models (BERT, RoBERTa) for accurate sentiment classification
- **Multi-Language Support**: Supports sentiment analysis in multiple languages
- **Emotion Detection**: Beyond positive/negative, detects specific emotions (joy, anger, fear, surprise)
- **Context-Aware Analysis**: Considers contextual information and sarcasm detection

### Event Tracking & Monitoring
- **Topic Clustering**: Groups related posts and mentions around specific events or topics
- **Trend Analysis**: Identifies emerging trends and their sentiment evolution over time
- **Geographic Analysis**: Maps sentiment and events by location for regional insights
- **Influencer Impact**: Tracks how key influencers affect sentiment trends

### Analytics & Visualization
- **Interactive Dashboards**: Real-time dashboards built with React and D3.js
- **Sentiment Timelines**: Visual representation of sentiment changes over time
- **Heat Maps**: Geographic sentiment distribution
- **Alert System**: Automated alerts for significant sentiment shifts or viral events

## Technical Architecture

### Data Pipeline
```
Data Sources → Kafka → Spark Streaming → ML Models → Database → API → Frontend
```

### Technology Stack
- **Backend**: Python, FastAPI, Apache Kafka, Apache Spark
- **Machine Learning**: PyTorch, Transformers, scikit-learn, spaCy
- **Database**: PostgreSQL, Redis (caching), Elasticsearch (search)
- **Frontend**: React.js, D3.js, Material-UI
- **Infrastructure**: Docker, Kubernetes, AWS/GCP
- **Monitoring**: Prometheus, Grafana

## Use Cases

### Brand Monitoring
- Track public sentiment towards brands, products, or services
- Monitor brand reputation during product launches or campaigns
- Identify potential PR crises before they escalate

### Political Analysis
- Monitor public opinion during elections or political events
- Track sentiment around policy announcements
- Analyze regional political sentiment differences

### Crisis Management
- Early detection of emerging crises or negative sentiment spikes
- Monitor public response to crisis management efforts
- Track recovery of public sentiment post-crisis

### Market Research
- Understand consumer sentiment towards products or services
- Identify emerging market trends and opportunities
- Competitive analysis through sentiment comparison

## Getting Started

### Prerequisites
- Python 3.8+
- Docker and Docker Compose
- Node.js 14+ (for frontend)
- API keys for data sources (Twitter API, Reddit API, News APIs)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Srimadhav-Seebu-Kumar/PulseCast-Event-Sentiment-Tracker.git
cd PulseCast-Event-Sentiment-Tracker
```

2. Set up environment variables:
```bash
cp .env.example .env
# Edit .env with your API keys and configuration
```

3. Start the services:
```bash
docker-compose up -d
```

4. Install Python dependencies:
```bash
pip install -r requirements.txt
```

5. Run database migrations:
```bash
python manage.py migrate
```

6. Start the application:
```bash
python app.py
```

The application will be available at `http://localhost:8000`

## API Documentation

The API documentation is available at `http://localhost:8000/docs` when the application is running.

### Key Endpoints
- `GET /api/sentiment/{topic}` - Get current sentiment for a topic
- `GET /api/trends` - Get trending topics and their sentiment
- `GET /api/events` - Get detected events and their sentiment timeline
- `POST /api/analyze` - Analyze custom text for sentiment

## Configuration

### Data Sources
Configure data sources in `config/sources.yaml`:
```yaml
twitter:
  api_key: "your_api_key"
  api_secret: "your_api_secret"
  enabled: true

reddit:
  client_id: "your_client_id"
  client_secret: "your_client_secret"
  enabled: true

news_api:
  api_key: "your_api_key"
  enabled: true
```

### ML Models
Configure sentiment analysis models in `config/models.yaml`:
```yaml
sentiment_model:
  name: "cardiffnlp/twitter-roberta-base-sentiment-latest"
  threshold: 0.7

emotion_model:
  name: "j-hartmann/emotion-english-distilroberta-base"
  enabled: true
```

## Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

### Development Setup
1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make your changes and add tests
4. Run tests: `pytest`
5. Submit a pull request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built with open-source NLP models from Hugging Face
- Inspired by social media analytics research
- Thanks to the community for feedback and contributions

## Contact

For questions or support, please open an issue or contact the maintainers.

---

**Note**: This project is for research and educational purposes. Please ensure compliance with platform terms of service and data privacy regulations when using this system.

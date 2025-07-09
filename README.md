# Forex-Anomaly-detector-
This repository contains a robust Python implementation of a multi-method anomaly detection system designed for financial time series data, specifically tailored for detecting anomalies in market data such as stock or forex prices
Advanced Financial Anomaly DetectionThis repository contains a robust Python implementation of a multi-method anomaly detection system designed for financial time series data, specifically tailored for detecting anomalies in market data such as stock or forex prices. The code integrates advanced statistical modeling, machine learning techniques, and visualization tools to identify unusual patterns in financial datasets with high accuracy and robustness.Key FeaturesData Acquisition and Caching: Uses yfinance to fetch historical market data (e.g., OHLCV data for tickers like EURUSD=X) and implements a caching mechanism to optimize data retrieval and reduce API calls.
Feature Engineering: Generates a comprehensive set of features, including:Technical indicators (e.g., SMA, EMA, RSI, Bollinger Bands).
Market microstructure features (e.g., VWAP, order flow imbalance).
Higher-order statistical moments (e.g., skewness, kurtosis).
Volatility and trend regime indicators.

Anomaly Detection Methods: Combines multiple complementary algorithms for robust anomaly detection:Mahalanobis Distance: Identifies outliers based on multivariate statistical distance.
Bayesian Change Point Detection: Detects structural breaks in time series using a Student-T model.
Isolation Forest: Uses tree-based isolation for anomaly detection.
DBSCAN Clustering: Identifies anomalies through density-based clustering.
PCA-Based Detection: Flags anomalies based on reconstruction errors in principal component analysis.
Ensemble Method: Combines results from all methods using weighted voting for improved reliability.

Numerical Stability: Includes a NumericalStabilityMixin to handle edge cases (e.g., division by zero, numerical overflow) using safe mathematical operations.
Visualization: Provides comprehensive visualizations using matplotlib and seaborn, including:Price series with anomaly markers.
Feature correlation heatmaps.
Anomaly detection method comparisons.
Distribution analysis, volatility regimes, PCA visualizations, and more.

Performance Optimization: Leverages numba for fast Mahalanobis distance calculations and parallel processing where applicable.
Error Handling and Logging: Implements robust error handling and logging for debugging and monitoring execution.

Key ComponentsDataManager: Handles data fetching, cleaning, and caching with validation to ensure data integrity.
AdvancedFeatureEngineer: Creates a rich feature set for anomaly detection, incorporating technical, statistical, and regime-based features.
AdvancedStudentT: Implements a multivariate Student-T distribution model with online parameter updates for robust Bayesian modeling.
RobustBayesianChangePointDetection: Performs online change point detection with numerical stability.
MultiMethodAnomalyDetector: Orchestrates multiple anomaly detection methods and combines their results into an ensemble.
AdvancedVisualization: Generates a comprehensive dashboard of plots to visualize anomalies, feature relationships, and detection performance.

UsageThe script is designed to be modular and configurable. Users can specify the financial instrument (e.g., EURUSD=X), time period, and interval for data retrieval. The AnomalyConfig dataclass allows customization of detection thresholds and parameters. The main workflow includes:Fetching and cleaning market data.
Generating features from raw data.
Fitting and applying multiple anomaly detection methods.
Visualizing results in a detailed dashboard saved as a JPEG file.
Exporting results to a CSV file for further analysis.

Examplepython

ticker = 'EURUSD=X'
data_manager = DataManager()
raw_data = data_manager.fetch_data(ticker, period='90d', interval='1h')
feature_engineer = AdvancedFeatureEngineer()
features = feature_engineer.create_features(raw_data)
detector = MultiMethodAnomalyDetector(AnomalyConfig())
detector.fit(features, training_size=1000)
anomaly_results = detector.detect_anomalies(features)
viz = AdvancedVisualization()
viz.plot_comprehensive_analysis(raw_data, features, anomaly_results, config, output_filename=f'anomaly_analysis_{ticker}.jpg')

DependenciesPython 3.x
numpy, pandas, matplotlib, seaborn, yfinance, scipy, sklearn, numba
Optional: logging, concurrent.futures for parallel processing

OutputVisualization: A comprehensive JPEG plot (anomaly_analysis_<ticker>.jpg) with multiple subplots analyzing anomalies, feature correlations, and risk metrics.
Results: A CSV file (anomaly_results_<ticker>.csv) containing raw data, engineered features, and anomaly detection results.
Console Summary: Prints the number and percentage of anomalies detected by each method.

Potential ApplicationsFinancial market monitoring for unusual trading patterns.
Risk management and portfolio analysis.
Algorithmic trading signal validation.
Research in financial time series analysis.

NotesThe code is optimized for numerical stability and performance but may require tuning of parameters (e.g., thresholds, window sizes) for specific datasets.
The visualization is designed for detailed analysis and can be customized by modifying the AdvancedVisualization class.
Ensure a stable internet connection for yfinance data retrieval.



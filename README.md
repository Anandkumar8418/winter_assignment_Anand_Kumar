

## Data Generation:

#### MerchantProfileGenerator: Creates merchant profiles with basic and additional fields
#### TransactionGenerator: Generates both normal and fraudulent transaction patterns

## Key characteristics of the generated data:

### Merchant Profiles:

Unique merchant IDs
Different business types
Random registration dates
Different GST statuses
20% are marked as fraudulent


### Normal Transactions:

50-200 transactions per merchant
Random dates within specified period
Amounts following normal distribution (mean=1000, std=300)
Random customer IDs


### Fraudulent Patterns:

#### a. Late Night Pattern:

Generates 20–50 transactions during unusual hours (11 PM to 4 AM).
Uses a higher average transaction amount (mean: 2000, std dev: 500).

####    b. High Velocity Pattern:

Picks a single "spike day" and generates 100–200 transactions on that day.
Distributes transactions across the 24 hours with higher average amounts (mean: 1500, std dev: 400).

#### c. Customer Concentration:


Assigns 80% of transactions to a single customer ID.
Generates 50–150 transactions with amounts normally distributed (mean: 1200, std dev: 300).

### Image of the generated data:
![Could Not Load Image](media/image.png)

##  Feature Engineering:

####    FeatureEngineer: Calculates and normalizes merchant features including:

Transaction velocity metrics
Time-based patterns
Amount distributions
Customer concentration




## Model Development:

####    FraudDetectionAutoencoder: Implements an autoencoder with:

3-layer encoder and decoder architecture
MSE-based reconstruction error
Automatic threshold calculation




##  Fraud Pattern Detection:

####    FraudPatternDetector: Implements specific detection rules for:

High velocity spikes
Odd-hour patterns
Customer concentration

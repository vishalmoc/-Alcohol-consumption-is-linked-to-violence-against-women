# Load necessary libraries
library(readxl)
library(ggplot2)
library(caret)
library(car)
library(randomForest)
library(rpart)
library(rpart.plot)

# Load the dataset
df <- read_xlsx("C:/Users/rajam/Downloads/nfhs_xl.xlsx")
# Select relevant columns
df_selected <- df[, c("Men age 15 years and above who consume alcohol (%)",
                      "Ever-married women age 18-49 years who have ever experienced spousal violence27 (%)",
                      "Ever-married women age 18-49 years who have experienced physical violence during any pregnancy (%)",
                      "Young women age 18-29 years who experienced sexual violence by age 18 (%)",
                      "Women (age 15-49 years) having a bank or savings account that they themselves use (%)",
                      "Female population age 6 years and above who ever attended school (%)")]

# Rename columns
colnames(df_selected) <- c("Men_Alcohol_Consumption", "Spousal_Violence", "Physical_Violence_Pregnancy",
                           "Sexual_Violence_Young", "Women_Bank_Account", "Female_Education")

# Convert non-numeric values to NA and remove missing values
df_selected <- as.data.frame(sapply(df_selected, as.numeric))
df_selected <- na.omit(df_selected)

# Check correlations to avoid multicollinearity
cor_matrix <- cor(df_selected)
print(cor_matrix)

# Check Variance Inflation Factor (VIF)
model_vif <- lm(Men_Alcohol_Consumption ~ ., data = df_selected)
vif(model_vif)

# Split data into training (70%) and testing (30%)
set.seed(123)
trainIndex <- createDataPartition(df_selected$Men_Alcohol_Consumption, p = 0.7, list = FALSE)
train_data <- df_selected[trainIndex, ]
test_data <- df_selected[-trainIndex, ]

# --- Model 1: Linear Regression ---
lm_model <- lm(Men_Alcohol_Consumption ~ ., data = train_data)
summary(lm_model)

# Predict and evaluate Linear Regression
lm_predictions <- predict(lm_model, newdata = test_data)
lm_rmse <- sqrt(mean((lm_predictions - test_data$Men_Alcohol_Consumption)^2))
lm_r2 <- summary(lm_model)$r.squared
cat("Linear Regression - RMSE:", lm_rmse, "R²:", lm_r2, "\n")

# --- Model 2: Decision Tree ---
tree_model <- rpart(Men_Alcohol_Consumption ~ ., data = train_data, method = "anova")
rpart.plot(tree_model)

# Predict and evaluate Decision Tree
tree_predictions <- predict(tree_model, newdata = test_data)
tree_rmse <- sqrt(mean((tree_predictions - test_data$Men_Alcohol_Consumption)^2))
cat("Decision Tree - RMSE:", tree_rmse, "\n")

# --- Model 3: Random Forest ---
rf_model <- randomForest(Men_Alcohol_Consumption ~ ., data = train_data, ntree = 500, importance = TRUE)

# Predict and evaluate Random Forest
rf_predictions <- predict(rf_model, newdata = test_data)
rf_rmse <- sqrt(mean((rf_predictions - test_data$Men_Alcohol_Consumption)^2))
cat("Random Forest - RMSE:", rf_rmse, "\n")

# Feature importance from Random Forest
importance(rf_model)
varImpPlot(rf_model)

# Compare Model Performance
performance <- data.frame(
  Model = c("Linear Regression", "Decision Tree", "Random Forest"),
  RMSE = c(lm_rmse, tree_rmse, rf_rmse),
  R2 = c(lm_r2, NA, NA)  # R² is not available for tree models
)
print(performance)

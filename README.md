# Ex.No.6 AI-Assisted Programming and Debugging
## Name : B V REVANTH KUMAR
## Register No.: 212224240023

# Aim:

To write and implement Python code using multiple AI tools for API interaction, output comparison, debugging, code optimization, complexity analysis, and unit-test generation, and to compare manual coding with AI-assisted coding.

# AI Tools Required:

* ChatGPT
* Google Gemini
* Claude

# Explanation:

AI-assisted programming uses Artificial Intelligence tools to generate, debug, optimize, and test computer programs. In this experiment, multiple AI tools are used to develop a Python application for a specific real-world problem. The generated programs are compared based on code quality, correctness, error handling, efficiency, and readability.

The selected application is **Smart Agriculture – Crop Monitoring and Weather Analysis**. The application collects crop and weather information from APIs, compares the obtained values, identifies possible risks, and generates suitable recommendations.

The experiment involves the following activities:

1. Generate Python code using multiple AI tools.
2. Interact with REST APIs and process JSON responses.
3. Compare outputs obtained from different sources.
4. Identify and correct possible bugs.
5. Optimize the generated code.
6. Analyze the time and space complexity.
7. Generate unit test cases.
8. Compare manual programming with AI-assisted programming.

# Selected Application Domain:

## Smart Agriculture – Crop and Weather Monitoring

The system obtains environmental information such as temperature, humidity, and soil moisture from monitoring APIs. The collected information is analyzed to identify unsuitable conditions for crop growth and generate recommendations.

# PROMPT DESIGN AND EXECUTION

## Stage 1: Python Code Generation

### Prompt Used:

**"Act as an experienced Python programmer. Develop a Python program for a smart agriculture monitoring system that retrieves temperature, humidity, and soil moisture data from two REST APIs. Parse the JSON responses, handle API errors properly, and display the important parameters in a readable format."**

### AI-Generated Python Code:

```python
import requests

def get_sensor_data(url):
    try:
        response = requests.get(url, timeout=5)
        response.raise_for_status()
        return response.json()

    except requests.exceptions.RequestException as error:
        print("API Error:", error)
        return None


def display_data(data, source):
    if data:
        print(f"\n{source}")
        print("Temperature:", data.get("temperature"))
        print("Humidity:", data.get("humidity"))
        print("Soil Moisture:", data.get("soil_moisture"))


api_1 = "https://example.com/api/farm1"
api_2 = "https://example.com/api/farm2"

data1 = get_sensor_data(api_1)
data2 = get_sensor_data(api_2)

display_data(data1, "Sensor API 1")
display_data(data2, "Sensor API 2")
```

The generated code uses the `requests` library to communicate with REST APIs. Exception handling is included to prevent the program from terminating when an API request fails.

---

# Stage 2: Comparing API Outputs

### Prompt Used:

**"Write a Python function to compare the temperature, humidity, and soil moisture values obtained from two agricultural monitoring APIs. Display the difference between the corresponding values and indicate whether the readings are similar or significantly different."**

### AI-Generated Code:

```python
def compare_readings(data1, data2):
    if not data1 or not data2:
        print("Insufficient data for comparison.")
        return

    temp_diff = abs(data1["temperature"] - data2["temperature"])
    humidity_diff = abs(data1["humidity"] - data2["humidity"])
    moisture_diff = abs(data1["soil_moisture"] - data2["soil_moisture"])

    print("\nComparison Results")
    print("Temperature Difference:", temp_diff)
    print("Humidity Difference:", humidity_diff)
    print("Soil Moisture Difference:", moisture_diff)

    if temp_diff > 5:
        print("Temperature readings differ significantly.")

    if humidity_diff > 10:
        print("Humidity readings differ significantly.")

    if moisture_diff > 15:
        print("Soil moisture readings differ significantly.")


compare_readings(data1, data2)
```

The comparison function calculates the absolute difference between corresponding sensor values. Thresholds are used to identify significant variations.

---

# Stage 3: Generating Actionable Insights

### Prompt Used:

**"Based on temperature, humidity, and soil moisture readings, generate Python logic that provides useful recommendations for farmers. Give warnings for high temperature, low soil moisture, and unsuitable humidity conditions."**

### AI-Generated Code:

```python
def generate_recommendations(data):
    if not data:
        return

    temperature = data.get("temperature", 0)
    humidity = data.get("humidity", 0)
    soil_moisture = data.get("soil_moisture", 0)

    print("\nRecommendations:")

    if temperature > 35:
        print("- High temperature detected. Consider providing shade.")

    if humidity < 40:
        print("- Low humidity detected. Monitor irrigation requirements.")

    if soil_moisture < 30:
        print("- Low soil moisture detected. Irrigation may be required.")

    if temperature <= 35 and humidity >= 40 and soil_moisture >= 30:
        print("- Environmental conditions are within the acceptable range.")


generate_recommendations(data1)
```

The program converts raw sensor information into simple and actionable recommendations.

---

# Stage 4: Bug Identification and Debugging

The AI-generated program was reviewed for possible programming errors and logical issues.

### Bugs / Issues Identified:

1. API URLs may be unavailable or return invalid data.
2. Required JSON keys may be missing.
3. The program may fail if sensor values are returned as strings.
4. Fixed threshold values may not be suitable for every crop.
5. Repeated API calls can increase execution time.

### Improved Code:

```python
def validate_data(data):
    required_fields = ["temperature", "humidity", "soil_moisture"]

    if not data:
        return False

    return all(field in data for field in required_fields)


def compare_readings(data1, data2):
    if not (validate_data(data1) and validate_data(data2)):
        print("Invalid or incomplete sensor data.")
        return

    differences = {
        "temperature": abs(float(data1["temperature"]) -
                           float(data2["temperature"])),

        "humidity": abs(float(data1["humidity"]) -
                        float(data2["humidity"])),

        "soil_moisture": abs(float(data1["soil_moisture"]) -
                             float(data2["soil_moisture"]))
    }

    return differences
```

The improved version validates the input before performing calculations and converts numerical values into floating-point numbers.

---

# Stage 5: Code Optimization

The generated code was optimized by:

* Dividing the program into reusable functions.
* Avoiding duplicate validation logic.
* Using dictionaries for storing comparison results.
* Using `timeout` while making API requests.
* Handling invalid or incomplete API responses.
* Separating API communication, comparison, and recommendation logic.

This makes the program more modular, readable, maintainable, and reliable.

# Stage 6: Complexity Analysis

For the comparison function, only a fixed number of sensor parameters are processed.

### Time Complexity:

**O(1)**

Since temperature, humidity, and soil moisture are fixed parameters, the number of operations remains constant.

### Space Complexity:

**O(1)**

Only a fixed-size dictionary is used to store the comparison results.

For a larger system containing **n sensor readings**, the corresponding comparison operation would have approximately **O(n)** time complexity.

# Stage 7: Unit Test Generation

### Prompt Used:

**"Generate Python unit tests using unittest for the sensor data validation and comparison functions. Include valid data, missing fields, and different sensor readings."**

### AI-Generated Unit Tests:

```python
import unittest


class TestSensorFunctions(unittest.TestCase):

    def test_valid_data(self):
        data = {
            "temperature": 30,
            "humidity": 60,
            "soil_moisture": 45
        }

        self.assertTrue(validate_data(data))

    def test_missing_field(self):
        data = {
            "temperature": 30,
            "humidity": 60
        }

        self.assertFalse(validate_data(data))

    def test_empty_data(self):
        self.assertFalse(validate_data(None))

    def test_comparison(self):
        data1 = {
            "temperature": 30,
            "humidity": 60,
            "soil_moisture": 40
        }

        data2 = {
            "temperature": 35,
            "humidity": 70,
            "soil_moisture": 50
        }

        result = compare_readings(data1, data2)

        self.assertEqual(result["temperature"], 5)
        self.assertEqual(result["humidity"], 10)
        self.assertEqual(result["soil_moisture"], 10)


if __name__ == "__main__":
    unittest.main()
```

The unit tests verify valid inputs, missing data, empty inputs, and correct calculation of sensor differences.

# ANALYSIS OF MULTIPLE AI TOOLS

| Criteria                 | ChatGPT         | Google Gemini     | Claude        |
| ------------------------ | --------------- | ----------------- | ------------- |
| Code Generation          | Well structured | Simple and direct | Detailed      |
| Error Handling           | Good            | Moderate          | Good          |
| Code Readability         | High            | High              | High          |
| Debugging                | Effective       | Effective         | Very detailed |
| Optimization Suggestions | Practical       | Basic             | Detailed      |
| Unit Test Generation     | Good            | Good              | Good          |
| Explanation              | Clear           | Concise           | Extensive     |

# OBSERVATIONS:

* All three AI tools were able to generate functional Python code from the given prompts.
* Clearly specifying the programmer persona improved the structure of the generated code.
* ChatGPT produced a balanced solution with readable functions and explanations.
* Gemini generated concise implementations that were easy to understand.
* Claude provided detailed explanations and suggested additional improvements.
* AI tools were useful for identifying missing input validation and improving error handling.
* Combining outputs from multiple AI tools helped in selecting better implementation approaches.

# MANUAL CODING VS AI-ASSISTED CODING

| Aspect            | Manual Coding                        | AI-Assisted Coding                |
| ----------------- | ------------------------------------ | --------------------------------- |
| Development Speed | Slower                               | Faster                            |
| Code Generation   | Written manually                     | Generated using prompts           |
| Debugging         | Requires manual inspection           | AI can identify possible bugs     |
| Testing           | Tests written manually               | Test cases can be generated       |
| Optimization      | Requires developer knowledge         | AI can suggest improvements       |
| Understanding     | Usually deeper during implementation | Requires review of generated code |
| Accuracy          | Depends on programmer                | Requires verification             |

AI-assisted programming significantly reduces development time, but the generated code must still be reviewed, tested, and validated by the programmer.

# Conclusion:

The experiment successfully demonstrated the use of multiple AI tools for Python code generation, API interaction, debugging, optimization, complexity analysis, and unit-test generation. Comparing the outputs of ChatGPT, Gemini, and Claude showed that each tool provides different approaches to solving the same programming problem. Proper prompt design and human verification are important for obtaining reliable and efficient AI-generated code.

# Result:

The Python program was successfully generated and analyzed using multiple AI tools. API interaction, output comparison, debugging, optimization, complexity analysis, and unit testing were performed successfully.

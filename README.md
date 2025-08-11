# Vision-Maths-OCR
**Vision Maths** is a machine learning project that recognizes handwritten mathematical expressions, converts them into digital text, evaluates them, and maps the result into a tactile Braille output for visually impaired users.

## Project Overview

The project’s core goal is to:
1. **Detect and segment** handwritten mathematical expressions from an image.
2. **Recognize each digit and operator** using a Convolutional Neural Network (CNN).
3. **Assemble and evaluate** the full mathematical expression.
4. **Convert the output** into Braille dot patterns and display them on a tactile hardware interface (Raspberry Pi + relays + solenoids).

## Workflow

1. **ML Model Benchmarking**  
   We compared different machine learning techniques for recognizing digits/operators:  
   - `KNN` – 97.05%  
   - `SVM` – 91.65%  
   - `Logistic Regression` – 92.00%  
   - `Decision Tree` – 87.76%  
   - **`CNN` – 99.07% (Chosen Model)**  

2. **Capstone CNN Model**  
   - Trained CNN on digits (0–9) and operators (+, -, *).
   - Input: 28×28 grayscale images.
   - Output: Class index → mapped to character.

3. **Expression Processing**  
   - Preprocess image: grayscale, threshold, dilation.
   - Find contours → isolate each symbol (digit/operator).
   - Classify each symbol with CNN.
   - Concatenate predictions into a string equation.
   - Safely evaluate the expression to get the result.
   - Example:  
     ```
     Input Image: handwritten "2+5"
     Predicted: "2+5"
     Result: "2+5=7"
     ```

4. **Braille Hardware Output** *(Post-OCR)*  
   After the digital expression is obtained, each character is mapped to a 0/1 Braille cell pattern.  
   These patterns are sent to a Raspberry Pi, which controls relays and 6 electromagnetic solenoids to physically raise Braille dots.  
   The user can then feel the Braille output representing the original expression and result.

## Installation

```bash
git clone https://github.com/NikhilSharma-30/Vision-Maths-OCR.git
cd Vision-Maths-OCR
pip install -r requirements.txt



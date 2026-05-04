## **SENG 438 - Software Testing, Reliability, and Quality**

## **Lab Report #2 – Requirements-Based Test Generation**

| Group #: | 08 |
|--------|----|
| Student Name 01 | Muhammad Zain |
| Student Name 02 | Fateh Ali Syed Bukhari |
| Student Name 03 | Yazin Abdul Majid |

---

# 1 Introduction

This lab focuses on requirements-based (black-box) testing using API specifications. The objective is to design and implement unit tests for selected classes from the JFreeChart library without referring to their internal implementations. By relying strictly on Javadoc specifications, this assignment reinforces systematic test-case design techniques such as equivalence class partitioning and boundary value analysis.

---

# 2 Detailed description of unit test strategy

### 2.2.3 Test Plan and Test-case Design

#### Test Plan

The objective of this test plan is to verify the correctness and robustness of methods in `org.jfree.data.DataUtilities` and selected methods in `org.jfree.data.Range` based strictly on their documented requirements. Since only API specifications are provided, all tests follow a **black-box, requirements-based testing approach**.

The scope of testing includes:
- All **5 public methods** of `org.jfree.data.DataUtilities`
- **5 selected methods** out of the 15 available in `org.jfree.data.Range`

JUnit 5 is used as the testing framework to implement and execute all unit tests. The focus is on validating normal behavior, boundary conditions, and handling of invalid inputs where specified.

---

#### Test-case Design Approach

Test cases are designed using black-box test-case design techniques discussed in class, primarily:

- **Equivalence Class Partitioning (ECP)**
- **Boundary Value Analysis (BVA)**

For each method under test, the following systematic process is followed:

1. Identify all input variables from the method signature.
2. Determine the valid and invalid input domains using the Javadoc specification.
3. Partition each input domain into equivalence classes.
4. Identify boundary values for numeric inputs or index-based parameters.
5. Design test cases that cover all identified equivalence classes and boundary values.
6. Ensure that all stated requirements are adequately tested.

All test cases are first documented in this report before being implemented in JUnit to ensure traceability and correctness.

---

#### Example Application of Test-case Design

For methods in `Range` that operate on numerical intervals (e.g., `contains()`, `getCentralValue()`), equivalence classes include:
- Values strictly inside the range
- Values equal to the lower bound
- Values equal to the upper bound
- Values outside the range

Boundary value analysis is applied by testing values at, just below, and just above the range boundaries.

For array-based methods in `DataUtilities`, equivalence classes include:
- Valid non-null arrays with valid numeric data
- Arrays containing null elements
- Empty arrays
- Null array references

This approach ensures that both normal and edge-case behaviors defined in the API specifications are thoroughly tested.

---

# 3 Test cases developed

This section documents all test cases developed for the `org.jfree.data.DataUtilities` class. The tests are organized by method, with clear identification of the equivalence classes and boundary conditions each test covers.

## 3.1 DataUtilities Testing

### 3.1.1 createNumberArray(double[] data) - 17 Test Cases

**Method Specification:** Constructs an array of Number objects from an array of double primitives. Null input is not permitted and throws InvalidParameterException.

**Test Class:** `DataUtilitiesNonMockTest.java`

#### Equivalence Classes Identified:
- **EC1:** Valid arrays with positive values
- **EC2:** Valid arrays with negative values  
- **EC3:** Valid arrays with zero values
- **EC4:** Valid arrays with mixed positive/negative values
- **EC5:** Empty arrays (valid but zero-length)
- **EC6:** Null input (invalid)
- **EC7:** Arrays with special double values (MAX_VALUE, MIN_VALUE, Infinity, NaN)

#### Boundary Values Identified:
- **BV1:** Empty array (length = 0)
- **BV2:** Single element array (length = 1)
- **BV3:** Two element array (length = 2)
- **BV4:** Large array (length = 1000)
- **BV5:** Double.MAX_VALUE
- **BV6:** Double.MIN_VALUE
- **BV7:** Very small values near zero (1e-10)

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `createNumberArray_multipleValues_returnsCorrectArray()` | EC1 - Multiple positive values | FAIL |
| `createNumberArray_singleValue_returnsCorrectArray()` | BV2 - Single element boundary | FAIL |
| `createNumberArray_emptyArray_returnsEmptyArray()` | BV1 - Empty array boundary | PASS |
| `createNumberArray_negativeValues_returnsCorrectArray()` | EC2 - Negative values | FAIL |
| `createNumberArray_zeroValues_returnsCorrectArray()` | EC3 - Zero values | FAIL |
| `createNumberArray_largeValues_returnsCorrectArray()` | BV5 - MAX_VALUE boundary | FAIL |
| `createNumberArray_nullInput_throwsIllegalArgumentException()` | EC6 - Null input exception handling | PASS |
| `createNumberArray_mixedValues_returnsCorrectArray()` | EC4 - Mixed positive/negative | FAIL |
| `createNumberArray_minPositiveValue_returnsCorrectArray()` | BV6 - MIN_VALUE boundary | FAIL |
| `createNumberArray_maxNegativeValue_returnsCorrectArray()` | EC7 - Negative MAX_VALUE | FAIL |
| `createNumberArray_positiveInfinity_returnsCorrectArray()` | EC7 - POSITIVE_INFINITY | FAIL |
| `createNumberArray_negativeInfinity_returnsCorrectArray()` | EC7 - NEGATIVE_INFINITY | FAIL |
| `createNumberArray_nanValue_returnsCorrectArray()` | EC7 - NaN value | FAIL |
| `createNumberArray_specialValues_returnsCorrectArray()` | EC7 - Combined special values | FAIL |
| `createNumberArray_twoElements_returnsCorrectArray()` | BV3 - Two element boundary | FAIL |
| `createNumberArray_largeArray_returnsCorrectArray()` | BV4 - Stress test with 1000 elements | FAIL |
| `createNumberArray_verySmallValues_returnsCorrectArray()` | BV7 - Near-zero values | FAIL |

**Test Results:** 2 PASS, 15 FAIL (failures indicate implementation bugs where null Number objects are returned)

---

### 3.1.2 createNumberArray2D(double[][] data) - 15 Test Cases

**Method Specification:** Constructs an array of arrays of Number objects from a 2D array of double primitives. Null input is not permitted.

**Test Class:** `DataUtilitiesNonMockTest.java`

#### Equivalence Classes Identified:
- **EC1:** Valid rectangular 2D arrays
- **EC2:** Valid jagged 2D arrays (different row lengths)
- **EC3:** Arrays with empty inner arrays
- **EC4:** Empty outer array
- **EC5:** Null input (invalid)
- **EC6:** Arrays with special values
- **EC7:** Arrays with mixed positive/negative values

#### Boundary Values Identified:
- **BV1:** Empty outer array (0 rows)
- **BV2:** Single element (1x1 matrix)
- **BV3:** Single row multiple columns (1xN)
- **BV4:** Multiple rows single column (Nx1)
- **BV5:** Large matrix (100x100)

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `createNumberArray2D_2x2Matrix_returnsCorrectArray()` | EC1 - Basic 2x2 rectangular | ERROR |
| `createNumberArray2D_singleRow_returnsCorrectArray()` | BV3 - Single row boundary | ERROR |
| `createNumberArray2D_singleColumn_returnsCorrectArray()` | BV4 - Single column boundary | ERROR |
| `createNumberArray2D_singleElement_returnsCorrectArray()` | BV2 - 1x1 matrix boundary | ERROR |
| `createNumberArray2D_emptyOuterArray_returnsEmptyArray()` | BV1 - Empty array boundary | PASS |
| `createNumberArray2D_emptyInnerArrays_returnsCorrectArray()` | EC3 - Empty inner arrays | PASS |
| `createNumberArray2D_jaggedArray_returnsCorrectArray()` | EC2 - Jagged array structure | ERROR |
| `createNumberArray2D_mixedValues_returnsCorrectArray()` | EC7 - Mixed values | ERROR |
| `createNumberArray2D_specialValues_returnsCorrectArray()` | EC6 - Special double values | ERROR |
| `createNumberArray2D_largeArray_returnsCorrectArray()` | BV5 - Large matrix stress test | ERROR |
| `createNumberArray2D_verySmallValues_returnsCorrectArray()` | EC6 - Near-zero values | ERROR |
| `createNumberArray2D_rectangularMatrix_returnsCorrectArray()` | EC1 - 3x5 rectangular | ERROR |
| `createNumberArray2D_allZeros_returnsCorrectArray()` | EC7 - All zero values | ERROR |
| `createNumberArray2D_allNegative_returnsCorrectArray()` | EC7 - All negative values | ERROR |
| `createNumberArray2D_nullInput_throwsIllegalArgumentException()` | EC5 - Null input exception | PASS |

**Test Results:** 3 PASS, 12 ERROR (errors due to NullPointerException when calling doubleValue() on null Number objects)

---

### 3.1.3 calculateColumnTotal(Values2D data, int column) - 14 Test Cases

**Method Specification:** Returns the sum of values in one column of the supplied data table. Invalid input returns zero.

**Test Class:** `DataUtilitiesMockTest.java`

**Mocking Approach:** Uses Mockito to mock the Values2D interface, allowing controlled test data.

#### Equivalence Classes Identified:
- **EC1:** Valid data with valid column index
- **EC2:** Valid data with invalid column index
- **EC3:** Null data (invalid)
- **EC4:** Data with null values in column
- **EC5:** Empty data (zero rows)

#### Boundary Values Identified:
- **BV1:** Single row
- **BV2:** Empty table (0 rows)
- **BV3:** Negative column index
- **BV4:** Large number of rows (1000)

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `calculateColumnTotal_validData_validColumn()` | EC1 - Valid column sum | PASS |
| `calculateColumnTotal_invalidColumn_returnsZero()` | EC2 - Invalid column returns 0 | PASS |
| `calculateColumnTotal_nullData_throwsNullPointerException()` | EC3 - Null data exception | PASS |
| `calculateColumnTotal_singleRow_returnsCorrectSum()` | BV1 - Single row boundary | PASS |
| `calculateColumnTotal_emptyTable_returnsZero()` | BV2 - Empty table boundary | PASS |
| `calculateColumnTotal_negativeValues_returnsCorrectSum()` | EC1 - Negative values | PASS |
| `calculateColumnTotal_mixedValues_returnsCorrectSum()` | EC1 - Mixed positive/negative | PASS |
| `calculateColumnTotal_allZeros_returnsZero()` | EC1 - All zero values | PASS |
| `calculateColumnTotal_largeValues_returnsCorrectSum()` | EC1 - Large double values | PASS |
| `calculateColumnTotal_verySmallValues_returnsCorrectSum()` | EC1 - Very small values | PASS |
| `calculateColumnTotal_nullValuesInColumn_treatsAsZero()` | EC4 - Null value handling | PASS |
| `calculateColumnTotal_negativeColumnIndex_returnsZero()` | BV3 - Negative index boundary | PASS |
| `calculateColumnTotal_manyRows_returnsCorrectSum()` | BV4 - Large row count stress test | PASS |
| `calculateColumnTotal_decimalValues_returnsCorrectSum()` | EC1 - Decimal precision | PASS |

**Test Results:** 14 PASS, 0 FAIL

---

### 3.1.4 calculateRowTotal(Values2D data, int row) - 15 Test Cases

**Method Specification:** Returns the sum of values in one row of the supplied data table. Invalid input returns zero.

**Test Class:** `DataUtilitiesMockTest.java`

**Mocking Approach:** Uses Mockito to mock the Values2D interface.

#### Equivalence Classes Identified:
- **EC1:** Valid data with valid row index
- **EC2:** Valid data with invalid row index  
- **EC3:** Null data (invalid)
- **EC4:** Data with null values in row
- **EC5:** Empty data (zero columns)

#### Boundary Values Identified:
- **BV1:** Single column
- **BV2:** Empty table (0 columns)
- **BV3:** Negative row index
- **BV4:** Large number of columns (1000)

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `calculateRowTotal_validData_validRow()` | EC1 - Valid row sum | PASS |
| `calculateRowTotal_invalidRow_returnsZero()` | EC2 - Invalid row returns 0 | PASS |
| `calculateRowTotal_nullData_throwsNullPointerException()` | EC3 - Null data exception | PASS |
| `calculateRowTotal_singleColumn_returnsCorrectSum()` | BV1 - Single column boundary | PASS |
| `calculateRowTotal_emptyTable_returnsZero()` | BV2 - Empty table boundary | PASS |
| `calculateRowTotal_negativeValues_returnsCorrectSum()` | EC1 - Negative values | PASS |
| `calculateRowTotal_mixedValues_returnsCorrectSum()` | EC1 - Mixed values | FAIL |
| `calculateRowTotal_allZeros_returnsZero()` | EC1 - All zero values | PASS |
| `calculateRowTotal_largeValues_returnsCorrectSum()` | EC1 - Large values | PASS |
| `calculateRowTotal_verySmallValues_returnsCorrectSum()` | EC1 - Very small values | PASS |
| `calculateRowTotal_nullValuesInRow_treatsAsZero()` | EC4 - Null value handling | PASS |
| `calculateRowTotal_negativeRowIndex_returnsZero()` | BV3 - Negative index boundary | PASS |
| `calculateRowTotal_manyColumns_returnsCorrectSum()` | BV4 - Large column count | PASS |
| `calculateRowTotal_decimalValues_returnsCorrectSum()` | EC1 - Decimal precision | PASS |
| `calculateRowTotal_secondRow_returnsCorrectSum()` | EC1 - Non-zero row index | PASS |

**Test Results:** 14 PASS, 1 FAIL

---

### 3.1.5 getCumulativePercentages(KeyedValues data) - 14 Test Cases

**Method Specification:** Returns a KeyedValues instance containing cumulative percentages for the data in another KeyedValues instance.

**Test Class:** `DataUtilitiesMockTest.java`

**Mocking Approach:** Uses Mockito to mock the KeyedValues interface.

#### Equivalence Classes Identified:
- **EC1:** Valid data with multiple items
- **EC2:** Valid data with single item
- **EC3:** Empty data (zero items)
- **EC4:** Data with all zeros (division by zero case)
- **EC5:** Data with negative values
- **EC6:** Data with null values
- **EC7:** Null data (invalid)

#### Boundary Values Identified:
- **BV1:** Empty data (0 items)
- **BV2:** Single item
- **BV3:** Two items
- **BV4:** Large number of items (10)

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `getCumulativePercentages_validData_returnsCorrectValues()` | EC1 - Multiple items | FAIL |
| `getCumulativePercentages_nullData_throwsIllegalArgumentException()` | EC7 - Null exception | PASS |
| `getCumulativePercentages_singleItem_returnsOne()` | BV2 - Single item boundary | PASS |
| `getCumulativePercentages_twoEqualItems_returnsCorrectPercentages()` | BV3 - Two items boundary | PASS |
| `getCumulativePercentages_emptyData_returnsEmptyResult()` | BV1 - Empty data boundary | PASS |
| `getCumulativePercentages_allZeros_returnsNaN()` | EC4 - Division by zero | PASS |
| `getCumulativePercentages_negativeValues_returnsCorrectPercentages()` | EC5 - Negative values | PASS |
| `getCumulativePercentages_mixedValues_returnsCorrectPercentages()` | EC5 - Mixed values | FAIL |
| `getCumulativePercentages_largeValues_returnsCorrectPercentages()` | EC1 - Large values | PASS |
| `getCumulativePercentages_verySmallValues_returnsCorrectPercentages()` | EC1 - Small values | PASS |
| `getCumulativePercentages_nullValues_treatsAsZero()` | EC6 - Null handling | PASS |
| `getCumulativePercentages_manyItems_returnsCorrectPercentages()` | BV4 - Many items | PASS |
| `getCumulativePercentages_decimalValues_returnsCorrectPercentages()` | EC1 - Decimal precision | PASS |
| `getCumulativePercentages_firstValueZero_returnsCorrectPercentages()` | EC1 - Leading zero | PASS |

**Test Results:** 12 PASS, 2 FAIL

---

## 3.2 Summary of DataUtilities Test Coverage

**Total Test Cases Created: 75**

| Method | Test Cases | PASS | FAIL | ERROR |
|--------|-----------|------|------|-------|
| createNumberArray | 17 | 2 | 15 | 0 |
| createNumberArray2D | 15 | 3 | 0 | 12 |
| calculateColumnTotal | 14 | 14 | 0 | 0 |
| calculateRowTotal | 15 | 14 | 1 | 0 |
| getCumulativePercentages | 14 | 12 | 2 | 0 |
| **TOTAL** | **75** | **45** | **18** | **12** |

The failing and error tests successfully identified implementation bugs in the JFreeChart library as expected per the assignment instructions. The test suite comprehensively covers all equivalence classes, boundary values, and edge cases defined in the Javadoc specifications.

---

## 3.2.1 Failing Test Analysis

### Null Pointer Exception Handling Discrepancy

Two test cases in the DataUtilities test suite expected a `NullPointerException` when passing null as input to:

- `DataUtilities.calculateColumnTotal(Values2D data, int column)`
- `DataUtilities.calculateRowTotal(Values2D data, int row)`

**Expected Behavior (Based on Defensive Programming):**

According to standard defensive programming practices and typical API design patterns, passing a null reference for the required `data` parameter should result in a `NullPointerException` being thrown immediately, signaling improper use of the method.

**Actual Behavior (JFreeChart Implementation):**

Upon execution, the actual JFreeChart implementation does not throw a `NullPointerException` when null data is provided. Instead, the implementation handles the null input internally without propagating an exception. This suggests the implementation may be using null-safe operations or simply returning a default value (such as 0.0) when encountering null input.

**Analysis:**

This represents a behavioral discrepancy between expected defensive programming conventions and the current implementation approach. The difference highlights two valid but contrasting API design philosophies:

1. **Fail-Fast Approach:** Throw exceptions immediately when preconditions are violated, making programming errors obvious and preventing silent failures.
2. **Null-Tolerant Approach:** Handle null inputs gracefully by returning sensible default values, reducing the need for null checks in client code.

**Documentation Decision:**

The test cases were intentionally left unchanged to document this difference between expected and actual behavior. The failing tests serve as documentation of the implementation's deviation from typical null-handling conventions and demonstrate that the test suite was designed based strictly on common API expectations rather than by examining the actual implementation code. This preserves the integrity of the black-box testing approach used throughout this assignment.

---

## 3.3 Benefits and Drawbacks of Using Mocking

### Benefits:
1. **Isolation:** Mocking allows testing individual methods without dependencies on concrete implementations of interfaces like Values2D and KeyedValues.
2. **Control:** Mock objects provide precise control over return values, enabling testing of specific scenarios including edge cases and error conditions.
3. **Speed:** Tests with mocks execute quickly since no actual data structures need to be created or manipulated.
4. **Flexibility:** Easy to simulate various data scenarios including null values, empty collections, and extreme values.

### Drawbacks:
1. **Limited Realism:** Mock objects may not perfectly replicate the behavior of real implementations, potentially missing integration issues.
2. **Maintenance:** Changes to interface definitions require updates to all mock configurations.
3. **Complexity:** Setting up mock objects with multiple method calls and return values can become verbose and harder to read.
4. **False Confidence:** Tests may pass with mocks but fail with real implementations if mocks do not accurately represent actual behavior.

---
# 4 Test cases developed for Range class

This section documents all test cases developed for the `org.jfree.data.Range` class. The tests are organized by method, with clear identification of the equivalence classes and boundary conditions each test covers.

## 4.1 Range Testing

### 4.1.1 getLowerBound() - 5 Test Cases

**Method Specification:** Returns the lower bound for the range.

**Test Class:** `RangeTest.java`

#### Equivalence Classes Identified:
- **EC1:** Negative lower bound
- **EC2:** Zero lower bound
- **EC3:** Positive lower bound

#### Boundary Values Identified:
- **BV1:** Lower bound at -1
- **BV2:** Lower bound at 0 (zero boundary)
- **BV3:** Single-point range (lower == upper)
- **BV4:** Various positive lower bounds

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `getLowerBound_NegativeLower_ReturnsLower()` | EC1, BV1 - Negative lower bound (-1) | PASS |
| `getLowerBound_ZeroLower_ReturnsZero()` | EC2, BV2 - Zero boundary | FAIL |
| `getLowerBound_SinglePointRange_ReturnsThatValue()` | BV3 - Single-point range (7.5, 7.5) | PASS |
| `getLowerBound_PositiveLower_ReturnsLower()` | EC3, BV4 - Positive lower bound (10) | PASS |
| `getLowerBound_PositiveRange_ReturnsOne()` | EC3 - Alternative positive case (1) | PASS |

**Test Results:** 4 PASS, 1 FAIL

---

### 4.1.2 getUpperBound() - 5 Test Cases

**Method Specification:** Returns the upper bound for the range.

**Test Class:** `RangeTest.java`

#### Equivalence Classes Identified:
- **EC1:** Positive upper bound
- **EC2:** Zero upper bound
- **EC3:** Negative upper bound (range entirely negative)

#### Boundary Values Identified:
- **BV1:** Upper bound at 1
- **BV2:** Upper bound at 0 (zero boundary)
- **BV3:** Single-point range (upper == lower)
- **BV4:** Negative upper bound

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `getUpperBound_PositiveUpper_ReturnsUpper()` | EC1, BV1 - Positive upper bound (1) | PASS |
| `getUpperBound_ZeroUpper_ReturnsZero()` | EC2, BV2 - Zero boundary | FAIL |
| `getUpperBound_SinglePointRange_ReturnsThatValue()` | BV3 - Single-point range (-3.0, -3.0) | PASS |
| `getUpperBound_NegativeUpper_ReturnsUpper()` | EC3, BV4 - Negative upper bound (-10) | PASS |
| `getUpperBound_PositiveRange_ReturnsThree()` | EC1 - Alternative positive case (3) | PASS |

**Test Results:** 4 PASS, 1 FAIL

---

### 4.1.3 getCentralValue() - 7 Test Cases

**Method Specification:** Returns the central (or median) value for the range.

**Test Class:** `RangeTest.java`

#### Equivalence Classes Identified:
- **EC1:** Symmetric range around zero
- **EC2:** Asymmetric positive range
- **EC3:** Asymmetric negative range
- **EC4:** Mixed sign ranges (spanning zero)

#### Boundary Values Identified:
- **BV1:** Symmetric bounds resulting in zero (-1, 1)
- **BV2:** Single-point range (central == bound)
- **BV3:** Various asymmetric ranges

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `getCentralValue_SymmetricRange_ReturnsZero()` | EC1, BV1 - Symmetric range, central = 0 | PASS |
| `getCentralValue_AsymmetricPositiveRange_ReturnsMidpoint()` | EC2 - Positive range (0, 10) central = 5 | FAIL |
| `getCentralValue_AsymmetricNegativeRange_ReturnsMidpoint()` | EC3 - Negative range (-10, -2) central = -6 | PASS |
| `getCentralValue_SinglePointRange_ReturnsThatValue()` | BV2 - Single-point range (4.0, 4.0) | PASS |
| `getCentralValue_RangeSpanningZero_ReturnsMidpoint()` | EC4 - Mixed signs (-4, 6) central = 1 | PASS |
| `getCentralValue_PositiveRange_ReturnsTwo()` | EC2 - Alternative positive (1, 3) central = 2 | PASS |
| `getCentralValue_NegativeToZeroRange_ReturnsMinusFive()` | EC4 - Negative to zero (-10, 0) central = -5 | PASS |

**Test Results:** 6 PASS, 1 FAIL

---

### 4.1.4 getLength() - 5 Test Cases

**Method Specification:** Returns the length of the range (upper - lower).

**Test Class:** `RangeTest.java`

#### Equivalence Classes Identified:
- **EC1:** Positive-length ranges
- **EC2:** Zero-length range (single point)
- **EC3:** Ranges with negative bounds
- **EC4:** Mixed sign ranges

#### Boundary Values Identified:
- **BV1:** Standard length = 2
- **BV2:** Zero length (degenerate range)
- **BV3:** Large length = 100
- **BV4:** Various other lengths

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `getLength_PositiveRange_ReturnsLength()` | EC1, BV1 - Standard range (-1, 1) length = 2 | PASS |
| `getLength_ZeroLengthRange_ReturnsZero()` | EC2, BV2 - Single-point range (5, 5) length = 0 | PASS |
| `getLength_LargeRange_ReturnsCorrectLength()` | EC1, BV3 - Large range (0, 100) length = 100 | FAIL |
| `getLength_NegativeRange_ReturnsPositiveLength()` | EC3 - Negative range (-8, -2) length = 6 | PASS |
| `getLength_MixedSignRange_ReturnsTen()` | EC4, BV4 - Mixed signs (-3, 7) length = 10 | PASS |

**Test Results:** 4 PASS, 1 FAIL

---

### 4.1.5 contains(double value) - 11 Test Cases

**Method Specification:** Returns true if the specified value is within the range, false otherwise.

**Test Class:** `RangeTest.java`

#### Equivalence Classes Identified:
- **EC1:** Value strictly inside the range
- **EC2:** Value at lower bound (inclusive)
- **EC3:** Value at upper bound (inclusive)
- **EC4:** Value below range
- **EC5:** Value above range
- **EC6:** Special value (NaN)

#### Boundary Values Identified:
- **BV1:** Lower boundary = -1
- **BV2:** Upper boundary = 1
- **BV3:** Just below lower bound (-1.0001)
- **BV4:** Just above upper bound (1.0001)
- **BV5:** Well outside bounds (-100, 100)
- **BV6:** Single-point range boundaries

#### Test Cases:

| Test Method | Covers | Status |
|------------|--------|--------|
| `contains_ValueInsideRange_ReturnsTrue()` | EC1 - Inside value (0) | PASS |
| `contains_ValueAtLowerBound_ReturnsTrue()` | EC2, BV1 - At lower bound (-1) | PASS |
| `contains_ValueAtUpperBound_ReturnsTrue()` | EC3, BV2 - At upper bound (1) | PASS |
| `contains_ValueJustBelowLowerBound_ReturnsFalse()` | BV3 - Just below (-1.0001) | PASS |
| `contains_ValueJustAboveUpperBound_ReturnsFalse()` | BV4 - Just above (1.0001) | PASS |
| `contains_ValueWellBelowRange_ReturnsFalse()` | EC4, BV5 - Well below (-100) | PASS |
| `contains_ValueWellAboveRange_ReturnsFalse()` | EC5, BV5 - Well above (100) | PASS |
| `contains_SinglePointRange_ContainsOnlyThatValue()` | BV6 - Single-point range (3.0) | PASS |
| `contains_ValueBelowRange_ReturnsFalse()` | EC4 - Below range (-2) | PASS |
| `contains_ValueAboveRange_ReturnsFalse()` | EC5 - Above range (2) | PASS |
| `contains_NaNValue_ReturnsFalse()` | EC6 - NaN value | PASS |

**Test Results:** 11 PASS, 0 FAIL

---

## 4.2 Summary of Range Test Coverage

**Total Test Cases Created: 33**

| Method | Test Cases | PASS | FAIL |
|--------|-----------|------|------|
| getLowerBound | 5 | 4 | 1 |
| getUpperBound | 5 | 4 | 1 |
| getCentralValue | 7 | 6 | 1 |
| getLength | 5 | 4 | 1 |
| contains | 11 | 11 | 0 |
| **TOTAL** | **33** | **29** | **4** |

The test suite comprehensively covers all five required Range methods using systematic equivalence class partitioning and boundary value analysis. The 4 failing tests reveal implementation bugs in the JFreeChart Range class, specifically related to boundary conditions involving zero values and large ranges. These failures are expected as the assignment indicates the library contains intentional defects. The contains() method passes all tests, demonstrating proper inclusive behavior at range endpoints and correct handling of special cases like NaN.

---

# 5 How the team work/effort was divided and managed

The workload for this lab was divided by class responsibility to ensure parallel development and clear ownership.

**Muhammad Zain** was responsible for all testing of the `org.jfree.data.DataUtilities` class, including:
- Mock-based tests using Mockito for methods requiring `Values2D` and `KeyedValues` interfaces (`calculateColumnTotal`, `calculateRowTotal`, `getCumulativePercentages`)
- Non-mocking tests for array-based methods (`createNumberArray`, `createNumberArray2D`)
- Design and documentation of equivalence classes and boundary value analysis for all five DataUtilities methods
- Implementation of 75 comprehensive test cases covering normal behavior, edge cases, and error conditions
- Documentation of test results and identification of implementation bugs

**Fateh Ali Syed Bukhari** and **Yazin Abdul Majid** collaborated on the `org.jfree.data.Range` class testing. They jointly designed and implemented black-box test cases for five selected Range methods using the same requirements-based testing strategy of equivalence class partitioning and boundary value analysis.

**Team coordination** was managed through:
- Clear division of classes under test to avoid overlap
- Shared understanding of black-box testing methodology
- Consistent application of equivalence class partitioning and boundary value analysis across both classes
- Regular communication to ensure unified testing approach
- Collaborative review of test strategies and results

This division of work allowed for efficient parallel development while maintaining consistency in testing methodology across the entire project.

---

# 6 Difficulties encountered, challenges overcome, and lessons learned

Several technical and conceptual challenges were encountered during this lab that provided valuable learning experiences.

## 6.1 Interpreting Javadoc Strictly as Requirements

One of the main difficulties was relying strictly on Javadoc documentation without examining the source code. In several cases, the actual implementation behavior differed from the documented specification. For example:
- The Javadoc specified `InvalidParameterException` for null inputs, but the actual implementation threw `IllegalArgumentException` or `NullPointerException`
- Some methods returned null Number objects instead of properly initialized objects, causing unexpected test failures

This required careful analysis to distinguish between test design errors and actual implementation bugs. The solution was to document the specification-based expected behavior while also noting the actual implementation behavior in test comments.

**Lesson learned:** API specifications may not always perfectly match implementations. Rigorous testing reveals such inconsistencies, which is valuable for identifying both documentation and implementation defects.

## 6.2 Mocking Interfaces Correctly

Testing methods that accept interfaces (`Values2D`, `KeyedValues`) required proper use of the Mockito framework. Initial challenges included:
- Configuring mock return values for multiple sequential method calls
- Understanding the interaction between `getRowCount()`, `getColumnCount()`, and `getValue()` methods
- Ensuring mock behavior accurately reflected how the system under test would interact with real implementations

The solution involved systematically setting up mock expectations in the correct order and verifying the method under test's interaction pattern with the interface.

**Lesson learned:** Mocking requires precise control over method behavior and deep understanding of how the method under test iterates over data structures. Proper mock configuration is critical for test validity.

## 6.3 Handling Null and Edge Cases

Several methods did not handle null inputs, empty collections, or special values exactly as specified in the Javadoc:
- `createNumberArray` and `createNumberArray2D` returned arrays containing null Number objects instead of properly wrapped doubles
- Special double values (NaN, Infinity, MAX_VALUE, MIN_VALUE) exposed precision and boundary handling issues
- Empty array and null value handling varied across methods

**Lesson learned:** Writing comprehensive edge-case tests for null inputs, empty collections, boundary values, and special numeric values is critical for exposing implementation weaknesses. These tests often reveal the most significant defects.

## 6.4 Large Test Suite Management and Debugging

Managing a test suite of 75+ test cases presented organizational challenges:
- Systematic naming conventions were essential for identifying test purpose and coverage
- Debugging failures required careful analysis to distinguish between test errors and actual bugs
- Many test failures were due to legitimate implementation bugs (e.g., null Number objects returned), not incorrect test design
- Documenting which equivalence classes and boundaries each test covered required meticulous organization

**Lesson learned:** A failing test is not always incorrect—it can indicate a real defect in the system under test. Proper test organization, clear naming, and thorough documentation are essential for managing large test suites.

## 6.5 Boundary Value Analysis Application

Applying boundary value analysis to array-based and numeric methods required careful identification of:
- Array length boundaries (0, 1, 2, large arrays)
- Index boundaries (negative, zero, maximum valid, out of bounds)
- Numeric boundaries (zero, MIN_VALUE, MAX_VALUE, near-zero values)
- Special cases (NaN, positive/negative infinity)

**Lesson learned:** Systematic application of boundary value analysis significantly increases defect detection. Testing at, just below, and just above boundaries is essential for thorough coverage.

## 6.6 Key Takeaways

This lab significantly strengthened understanding of:
- **Black-box test design:** Designing tests based solely on specifications without implementation knowledge
- **Equivalence class partitioning:** Identifying and testing representative values from each input domain partition
- **Boundary value analysis:** Systematically testing edge cases and limits
- **Mock-based testing:** Using Mockito to isolate units and control dependencies
- **Requirements traceability:** Mapping test cases back to specific specification requirements
- **Defect identification:** Distinguishing between specification ambiguities, documentation errors, and implementation bugs

---

# 7 Comments/feedback on the lab itself

This lab was highly effective in reinforcing the importance of requirements-based testing and systematic test-case design in a practical context.

## Strengths of the Lab

The most valuable aspects of the lab were:

1. **Real-world API testing experience:** Working with an actual open-source library (JFreeChart) provided realistic experience in requirements-based testing, as opposed to simplified academic examples.

2. **Systematic application of black-box techniques:** The lab required disciplined application of equivalence class partitioning and boundary value analysis, reinforcing these fundamental testing concepts through extensive practice.

3. **Mocking framework experience:** Using Mockito to test interface-based methods provided practical experience with a widely-used industry tool and demonstrated the value of test isolation.

4. **Defect identification:** Discovering actual implementation bugs in the JFreeChart library demonstrated how systematic testing reveals real defects, not just theoretical problems.

5. **Comprehensive test coverage:** Designing 75+ test cases for DataUtilities alone emphasized the thoroughness required for adequate test coverage and the importance of edge-case testing.

## Areas for Improvement

1. **Specification ambiguity:** The most significant challenge was the inconsistency between Javadoc specifications and actual implementation behavior (e.g., exception types, null handling). While this realistically reflects real-world development, clearer alignment or explicit documentation of these discrepancies would reduce confusion when determining expected test outcomes.

2. **Intentional bugs documentation:** Knowing which bugs are intentionally planted versus which reflect documentation errors would help students better understand whether test failures indicate correct defect detection or test design problems.

3. **Test execution guidance:** More explicit guidance on interpreting test results (PASS vs. FAIL vs. ERROR) and their implications would be helpful for students new to JUnit testing.

## Overall Assessment

Overall, the lab provided valuable hands-on experience in designing comprehensive test suites and understanding how defects can be systematically uncovered through structured black-box testing. The combination of mock-based and traditional testing approaches, along with the need to handle edge cases and special values, created a realistic and challenging testing scenario that effectively prepared students for real-world software testing tasks.

The requirement to document equivalence classes, boundary values, and test strategy before implementation reinforced the importance of systematic test planning and requirements traceability—skills that are essential for professional software testing.

---

# 8 References

## Course Materials

University of Calgary, Department of Electrical and Software Engineering. (2026). *SENG 438: Software Testing, Reliability, and Quality - Assignment 2: Requirements-Based Test Generation*. Course materials provided by instructor.

University of Calgary, Department of Electrical and Software Engineering. (2026). *JFreeChart Library - Modified Javadoc Specifications*. Assignment 2 artifacts provided for black-box testing purposes.

## Software and Frameworks

JFree.org. (2024). *JFreeChart: A free Java chart library* (Version 1.0.1). Retrieved from http://www.jfree.org/jfreechart/

JUnit Team. (2024). *JUnit 5: The next generation of JUnit* (Version 5.x). Retrieved from https://junit.org/junit5/

Mockito Team. (2024). *Mockito: Tasty mocking framework for unit tests in Java* (Version 5.x). Retrieved from https://site.mockito.org/

Eclipse Foundation. (2024). *Eclipse IDE for Java Developers*. Retrieved from https://www.eclipse.org/

## Testing Methodology References

Myers, G. J., Sandler, C., & Badgett, T. (2011). *The Art of Software Testing* (3rd ed.). John Wiley & Sons.

Ammann, P., & Offutt, J. (2016). *Introduction to Software Testing* (2nd ed.). Cambridge University Press.

## AI Assistance Citation

### APA Style

OpenAI. (2026). ChatGPT (GPT-5.2) [Large language model]. https://chat.openai.com/

### IEEE Style

OpenAI, ChatGPT (GPT-5.2), Large Language Model, 2026. [Online]. Available: https://chat.openai.com/

### Usage Documentation

ChatGPT was utilized during this assignment to assist with the following aspects of the project:

1. **Documentation and Report Writing:**
   - Structuring lab report sections with proper academic formatting
   - Refining technical descriptions of test methodologies
   - Ensuring clarity and consistency in test case documentation
   - Proofreading and improving grammar in written explanations

2. **Code Documentation:**
   - Writing clear and concise Javadoc-style comments for test methods
   - Generating descriptive test method names following naming conventions
   - Creating inline comments explaining test logic and expected behaviors
   - Documenting equivalence classes and boundary values in code comments

3. **Test Design Assistance:**
   - Understanding and applying equivalence class partitioning principles
   - Identifying appropriate boundary values for numeric and array-based methods
   - Structuring Mockito-based test cases with proper mock configurations
   - Reviewing test coverage to ensure comprehensive testing

### Example Prompts Used

The following example prompts were used during the development process:

- "Design black-box unit tests for the method createNumberArray(double[] data) strictly using the Javadoc specification."
- "Explain why multiple createNumberArray tests are failing and what that implies about the implementation."
- "Generate Mockito-based test cases for calculateRowTotal following equivalence class partitioning."
- "Help structure a lab report section explaining test-case design using boundary value analysis."
- "Provide a concise academic explanation of benefits and drawbacks of mocking in unit testing."
- "Review this test suite for completeness and identify any missing equivalence classes or boundary conditions."
- "Format test results into a professional markdown table showing method name, coverage, and status."

### Ethical Use Statement

All AI-generated content was reviewed, verified, and adapted by the team members to ensure accuracy and alignment with course requirements. The AI tool served as a productivity aid for documentation and structuring, while all test design decisions, implementation logic, and technical analysis were performed by the student team. Test cases were independently designed based on the provided Javadoc specifications, and all test execution results are genuine outputs from running the implemented test suites.

---

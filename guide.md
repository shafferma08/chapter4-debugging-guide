### Guide for Tuba Farm Equipment Page Fixes

1. **Add "use strict" at the top of the file**:
   - Add:
     ```javascript
     "use strict";
     ```

2. **Correct the global variables declarations**:
   - Change:
     ```javascript
     acresComplete = true;
     et fuelComplete = true;
     ```
   - To:
     ```javascript
     let acresComplete = true;
     let fuelComplete = true;
     ```

3. **Fix the syntax errors in the variable assignments**:
   - Change:
     ```javascript
     let monthsFieldset  document.getElementsByTagName("fieldset")[2];
     let fuelFieldset = document.getElementsByTagName("fieldset)[3];
     ```
   - To:
     ```javascript
     let monthsFieldset = document.getElementsByTagName("fieldset")[2];
     let fuelFieldset = document.getElementsByTagName("fieldset")[3];
     ```

4. **Add error handling in `verifyAcres` function**:
   - Change:
     ```javascript
     function verifyAcres() {
        testFormCompleteness();
     }
     ```
   - To:
     ```javascript
     function verifyAcres() {
        try {
           if (!(acresBox.value > 0)) throw "Enter a positive acreage";
           testFormCompleteness();
        } catch(error) {
           messageElement.innerHTML = error;
           messageHeadElement.innerHTML = "";
        }
     }
     ```

5. **Add error handling in `verifyMonths` function**:
   - Change:
     ```javascript
     function verifyMonths() {
        testFormCompleteness();
     }
     ```
   - To:
     ```javascript
     function verifyMonths() {
        try {
           if (!(monthsBox.value >= 1 && monthsBox.value <= 12)) 
              throw "Enter months between 1 and 12";
           testFormCompleteness();
        } catch(error) {
           messageElement.innerHTML = error;
           messageHeadElement.innerHTML = "";      
        }
     }
     ```

6. **Correct the logic in `createRecommendation` function**:
   - Change:
     ```javascript
     if (acresBox.value >= 5000) { // 5000 acres or less, no crop test needed
        if (monthsBox.value <= 10) { // 10+ months of farming per year
           messageHeadElement.innerHTML = "E3250";
           messageElement.innerHTML = E3250Desc;
        } else { // 9 or fewer months per year
           messageHeadElement.innerHTML = "E2600";
           messageElement.innerHTML = E2600Desc;
        }
     } else { // more than 5000 acres
        if (monthsBox.value <= 9) { // 9 or fewer months per year, no crop test needed
           messageHeadElement.innerHTML = "W1205";
           messageElement.innerHTML = W1205Desc;
        } else { // 10+ months of farming per year
           if (document.getElementById("wheat").checked || document.getElementById("corn").checked || document.getElementById("soy").checked) {
              messageHeadElement.innerHTML = "W2500";
              messageElement.innerHTML = W2500Desc;
           } else {
              messageHeadElement.innerHTML = "W2550";
              messageElement.innerHTML = W2550Desc;
           }
        }
     }
     ```
   - To:
     ```javascript
     if (acresBox.value <= 5000) { // 5000 acres or less, no crop test needed
        if (monthsBox.value >= 10) { // 10+ months of farming per year
           messageHeadElement.innerHTML = "E3250";
           messageElement.innerHTML = E3250Desc;          
        } else { // 9 or fewer months per year
           messageHeadElement.innerHTML = "E2600";
           messageElement.innerHTML = E2600Desc; 
        }
     } else { // more than 5000 acres
        if (monthsBox.value <= 9) { // 9 or fewer months per year, no crop test needed
           messageHeadElement.innerHTML = "W1205";        
           messageElement.innerHTML = W1205Desc;
        } else { // 10+ months of farming per year
           if (document.getElementById("wheat").checked || document.getElementById("corn").checked || document.getElementById("soy").checked) {
              messageHeadElement.innerHTML = "W2500";
              messageElement.innerHTML = W2500Desc;
           } else {
              messageHeadElement.innerHTML = "W2550";
              messageElement.innerHTML = W2550Desc;
           }
        }
     }
     ```

7. **Correct the model name concatenation logic**:
   - Change:
     ```javascript
     if (document.getElementById("E85").checked) { // add suffix to model name based on fuel choice
        messageHeadElement.innerHTML += "E";
     } else if (document.getElementById("biodiesel").checked) {
        messageHeadElement.innerHTML = "B";
     } else {
        messageHeadElement.innerHTML += "D";  
     }
     ```
   - To:
     ```javascript
     if (document.getElementById("E85").checked) { // add suffix to model name based on fuel choice
        messageHeadElement.innerHTML += "E";
     } else if (document.getElementById("biodiesel").checked) {
        messageHeadElement.innerHTML += "B";
     } else {
        messageHeadElement.innerHTML += "D";  
     }
     ```

# HTML in VsCode Tips and Tricks
## Balancing
- Tracking, selecting and adjusting blocks of markdown in large HTML files can be a real pain at times. A quick but useful tool already integrated in vsCode is the balancing functions which help with auto selecting blocks of your HTML, reducing manual parse time and enhancing your productivity. 
### Balance (Outward)
- "Balance Outward" is one of the two commands in vscode to help support you in your HTML endeavors. It can quickly be utilized just like any other command in vscode by opening up the vscode command terminal with **"Ctrl + shift + P"**, typing in **"balance outward"** and slapping that enter button.
  - **Result:** The element in which your cursor lies will be selected from start tag to end tag **Inclusively**. 

    ![image.png](./images/Screenshot%202022-08-29%20204046.png)

### Balance (Inward)
- "Balance Inward" is the second of the two and can be utilized the same as **Balance Outward**, by using **"Ctrl + shift + p"** to open up the vscode command terminal and entering **"balance inward"**.
  - **Result:** All html elements inside of the nearest element in relation to your cursor will be selected from start tag to end tag.
![image.png](./images/Screenshot%202022-08-29%20204520.png)
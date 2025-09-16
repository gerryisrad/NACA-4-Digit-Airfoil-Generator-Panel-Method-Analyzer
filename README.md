# NACA-4-Digit-Airfoil-Generator-Panel-Method-Analyzer
A MATLAB script that generates NACA 4-digit airfoil geometries and calculates their pressure distribution using a source panel method.
# NACA 4-Digit Airfoil Generator & Panel Method Analyzer

This MATLAB script provides a tool for aerodynamic analysis by generating the coordinates of any NACA 4-digit series airfoil and then calculating its surface pressure distribution using a source panel method for potential flow.



---

## 📜 About The Project

The script is divided into two main parts:

1.  **Airfoil Geometry Generation:** Based on user input for a NACA 4-digit airfoil (e.g., NACA 2412), it calculates the coordinates of the upper and lower surfaces using the standard analytical equations for camber and thickness distributions.
2.  **Aerodynamic Analysis:** It then uses these coordinates to discretize the airfoil surface into a series of flat panels. By applying the principles of potential flow, it solves for the source strengths on each panel that satisfy the no-penetration boundary condition. From this, it calculates the tangential velocity and the coefficient of pressure ($C_p$) at each panel's control point.

This project is primarily intended for educational purposes to demonstrate the fundamentals of airfoil design and computational fluid dynamics (CFD) through the panel method.

---

## ⚙️ How to Use

1.  Ensure you have **MATLAB** installed.
2.  Save the entire script as a `.m` file (e.g., `naca_analyzer.m`).
3.  Run the script from the MATLAB command window or editor.
4.  You will be prompted in the command window to enter the airfoil number:
    ```matlab
    Enter The Airfoil Number in Raw Vector as [x x x x]:
    ```
5.  Enter the four digits as a MATLAB vector. For example, for a **NACA 2412**, you would type:
    ```matlab
    [2 4 1 2]
    ```
6.  Press **Enter**. The script will execute and automatically produce two plots:
    * **Figure 1:** The airfoil geometry, showing the upper and lower surfaces along with the mean camber line.
    * **Figure 2:** The pressure coefficient ($C_p$) distribution around the airfoil surface.

The script will also save the airfoil coordinates to a `.mat` file named `2412d.mat` in the current directory.

---

## 🔬 Underlying Theory

### NACA 4-Digit Series

The designation of a NACA 4-digit airfoil specifies its geometric properties:

* **First digit (M):** Maximum camber as a percentage of the chord length ($M = \text{NACA(1)} / 100$).
* **Second digit (P):** Position of the maximum camber from the leading edge in tenths of the chord ($P = \text{NACA(2)} / 10$).
* **Last two digits (XX):** Maximum thickness as a percentage of the chord length ($T = \text{NACA(3,4)} / 100$).

The script uses the standard analytical equations to define the mean camber line ($y_c$) and the thickness distribution ($y_t$), which are then combined to generate the final airfoil coordinates ($x_u, y_u, x_l, y_l$).

### Source Panel Method

The panel method is a technique used in potential flow theory to model the flow around a body. The process involves:

1.  **Discretization:** The airfoil surface is approximated by a finite number of straight-line segments called panels.
2.  **Influence Coefficients:** The velocity induced at the control point (midpoint) of one panel by a source distribution on another panel is calculated. This forms a matrix of influence coefficients.
3.  **Boundary Condition:** The **flow tangency** or **no-penetration** condition is applied. This states that the component of the flow velocity normal to the surface must be zero at every control point.
4.  **Solving:** This boundary condition results in a system of linear algebraic equations, $A \cdot \lambda = b$, where $\lambda$ is the vector of unknown source strengths. Solving this system yields the source strength for each panel.
5.  **Post-Processing:** With the source strengths known, the tangential velocity and, subsequently, the coefficient of pressure ($C_p = 1 - (V_t/V_\infty)^2$) can be calculated for each panel.



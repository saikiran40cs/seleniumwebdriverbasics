# Junit {#junit}

---

TestNG improves upon some of the drawbacks in Junit, which we will discuss later. Below is a sample Junit test.

```
package code;

import junit.framework.TestCase;

public class Junit extends TestCase {

    protected int value1, value2;

    // assigning the values
    protected void setUp() {
        value1 = 6;
        value2 = 2;
    }

    // test method to add two values
    public void testAdd() {
        Calculator calc = new Calculator();
        assertTrue(8 == calc.add(value1, value2));
        assertTrue(4 == calc.subtract(value1, value2));
        assertTrue(12 == calc.multiply(value1, value2));
        assertFalse(20 == calc.divide(value1, value2));
    }

}

class Calculator {

    public int add(int num1, int num2) {
        return num1 + num2;
    }

    public int subtract(int num1, int num2) {
        return num1 - num2;
    }

    public int multiply(int num1, int num2) {
        return num1 * num2;
    }

    public int divide(int num1, int num2) {
        return num1 / num2;
    }
}
```





package calculadora;


import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.JTextField;
public class CalculatorFrame extends JFrame implements ActionListener {
    JTextField textField;
    double num1, num2, result;
    char operator;

    public CalculatorFrame() {
        setTitle("Calculadora");
        setSize(300, 400);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JPanel panel = new JPanel();
        textField = new JTextField(10);
        panel.add(textField);

        String[] buttonLabels = {"1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "+", "-", "*", "/", "C",  "=", };
        for (String label : buttonLabels) {
            JButton button = new JButton(label);
            button.addActionListener(this);
            panel.add(button);
        }

        add(panel);
        setVisible(true);
    }

    @Override
    public void actionPerformed(ActionEvent e) {
        String actionCommand = e.getActionCommand();
        char input = actionCommand.charAt(0);

        if (Character.isDigit(input)) {
            textField.setText(textField.getText() + input);
        } else if (actionCommand.equals("C")) {
            textField.setText("");
        } else if (actionCommand.equals("=")) {
            num2 = Double.parseDouble(textField.getText());
            switch (operator) {
                case '+':
                    result = num1 + num2;
                    break;
                case '-':
                    result = num1 - num2;
                    break;
                case '*':
                    result = num1 * num2;
                    break;
                case '/':
                    result = num1 / num2;
                    break;
            }
            textField.setText(String.valueOf(result));
        } else {
            num1 = Double.parseDouble(textField.getText());
            operator = input;
            textField.setText("");
        }
    }

    public static void main(String[] args) {
        new CalculatorFrame();
    }
}
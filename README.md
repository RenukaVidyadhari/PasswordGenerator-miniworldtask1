# PasswordGenerator-miniworldtask1

/*Password Length:
    Decide on the minimum and maximum length of the password. A good range is usually between 8 and 16 characters.

Character Sets:
    Include a mix of character types to enhance security:

Uppercase letters (A-Z)

Lowercase letters (a-z)

Digits (0-9)

Special symbols (!, @, #, $, etc.)

Exclusion of Ambiguous Characters: 

    Exclude characters that can be mistaken for others (e.g., 'l' and '1', 'O' and '0', etc.), as they can cause confusion.

Cryptographically Secure Randomness: 

    Use a cryptographically secure random number generator to ensure the randomness of the generated passwords. In Java, you can use the java.security.SecureRandom class.

Avoid Common Patterns: 

    Avoid patterns like repeated characters or sequences (e.g., "123456", "aaaaaa", etc.) that could weaken the password.

No Personal Information:

    Do not include any personal information or easily guessable patterns like birthdates, names, etc.

Avoid Dictionary Words: 

    Avoid using dictionary words or common phrases, as they can be susceptible to dictionary attacks.

Configurability: 
   
   Make the password generation algorithm configurable so that you can adjust the character sets and other parameters easily.

Entropy:
   Aim for a password with high entropy, which means it should have a large number of possible combinations. This makes it difficult for attackers to guess or crack the password.
*/

//importing the packages according to conditions involved.
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.security.SecureRandom;

//implementing the class method to generate a password and declaring the varaibles for characters and for gui.

public class PasswordGeneratorGUI extends JFrame {

    private final String LOWERCASE = "abcdefghijklmnopqrstuvwxyz";
    private final String UPPERCASE = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    private final String DIGITS = "0123456789";
    private final String SPECIAL_CHARACTERS = "!@#$%^&*()-_=+[]{}|;:,.<>?";
//a Jlabel is a GUI component used to display text or an image that provides information to the user.
    private JLabel lengthLabel;
//A JSpinner is a GUI component in Java that allows users to input a value by either typing it or using increment/decrement buttons.
    private JSpinner lengthSpinner;
    private JCheckBox lowercaseCheckBox;
    private JCheckBox uppercaseCheckBox;
    private JCheckBox digitsCheckBox;
    private JCheckBox specialCharsCheckBox;
    private JButton generateButton;
    private JTextArea passwordTextArea;

//implementing the constructor to defining the variables declared in class

    public PasswordGeneratorGUI() {
        setTitle("Password Generator");
        setSize(400, 300);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        JPanel mainPanel = new JPanel(new GridLayout(7, 1));

        lengthLabel = new JLabel("Password Length:");
        lengthSpinner = new JSpinner(new SpinnerNumberModel(12, 1, 50, 1));
        lowercaseCheckBox = new JCheckBox("Include Lowercase");
        uppercaseCheckBox = new JCheckBox("Include Uppercase");
        digitsCheckBox = new JCheckBox("Include Digits");
        specialCharsCheckBox = new JCheckBox("Include Special Characters");
        generateButton = new JButton("Generate Password");
        passwordTextArea = new JTextArea(3, 20);
        passwordTextArea.setEditable(false);

        generateButton.addActionListener(new ActionListener() {
//annotations are used by tools or frameworks to generate code, perform validations, or enhance code readability.    
            @Override
            public void actionPerformed(ActionEvent e) {
                generatePassword();
            }
        });

        mainPanel.add(lengthLabel);
        mainPanel.add(lengthSpinner);
        mainPanel.add(lowercaseCheckBox);
        mainPanel.add(uppercaseCheckBox);
        mainPanel.add(digitsCheckBox);
        mainPanel.add(specialCharsCheckBox);
        mainPanel.add(generateButton);
        mainPanel.add(passwordTextArea);

        add(mainPanel);
        setVisible(true);
    }

//implementing the private method for conditions which can generates the message boxes.

    private void generatePassword() {
        int length = (int) lengthSpinner.getValue();
        String characters = "";
        if (lowercaseCheckBox.isSelected()) {
            characters += LOWERCASE;
        }
        if (uppercaseCheckBox.isSelected()) {
            characters += UPPERCASE;
        }
        if (digitsCheckBox.isSelected()) {
            characters += DIGITS;
        }
        if (specialCharsCheckBox.isSelected()) {
            characters += SPECIAL_CHARACTERS;
        }
        if (characters.isEmpty()) {
            JOptionPane.showMessageDialog(this, "Please select at least one character set.");
            return;
        }
        StringBuilder password = new StringBuilder();
        SecureRandom random = new SecureRandom();

        for (int i = 0; i < length; i++) {
            int randomIndex = random.nextInt(characters.length());
            password.append(characters.charAt(randomIndex));
        }

        passwordTextArea.setText(password.toString());
    }

//implementing the main function for object creation and to access the methods and variables.

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new PasswordGeneratorGUI();
            }
        });
    }
}

# OOP-project
package com.mycompany.tttt;
import javax.swing.*;
import java.awt.*;
import java.util.ArrayList;
import java.io.FileWriter;
import java.io.IOException;
/**
 *
 * @author Waqas Laptop
 */
// Abstract Player class (abstraction + encapsulation)
abstract class Player {
    private String name;
    private int age;
    private String type;

    public void setName(String name) { this.name = name; }
    public void setAge(int age) { this.age = age; }
    public void setType(String type) { this.type = type; }

    public String getName() { return name; }
    public int getAge() { return age; }
    public String getType() { return type; }

    public abstract String getStats(); //Abstract method: subclasses must provide their own getStats method
}

// Batsman class (inheritance)
class Batsman extends Player {
    private int runs, matches;
    private float average;

    public void setBatsmanStats(int runs, int matches, float average) {
        this.runs = runs;
        this.matches = matches;
        this.average = average;
    }

    public String getStats() {
        return String.format("Player Type: Batsman\nName: %s\nAge: %d\nRuns: %d\nMatches: %d\nBatting Avg: %.2f",
                getName(), getAge(), runs, matches, average);
    }
}

// Bowler class
class Bowler extends Player {
    private int wickets, matches;
    private float economy;

    public void setBowlerStats(int wickets, int matches, float economy) {
        this.wickets = wickets;
        this.matches = matches;
        this.economy = economy;
    }

    public String getStats() {
        return String.format("Player Type: Bowler\nName: %s\nAge: %d\nWickets: %d\nMatches: %d\nEconomy: %.2f",
                getName(), getAge(), wickets, matches, economy);
    }
}

// Allrounder class
class Allrounder extends Player {
    private int runs, wickets, matches;
    private float average, economy;

    public void setAllrounderStats(int runs, int wickets, int matches, float average, float economy) {
        this.runs = runs;
        this.wickets = wickets;
        this.matches = matches;
        this.average = average;
        this.economy = economy;
    }

    @Override
    public String getStats() {
        return String.format("Player Type: Allrounder\nName: %s\nAge: %d\nRuns: %d\nWickets: %d\nMatches: %d\nBatting Avg: %.2f\nEconomy: %.2f",
                getName(), getAge(), runs, wickets, matches, average, economy);
    }
}

// Main GUI class
public class Tttt extends JFrame {
    private JComboBox<String> typeBox;
    private JTextField nameField, ageField, runsField, wicketsField, matchesField, avgField, ecoField;
    private JTextArea outputArea;
    private ArrayList<Player> players = new ArrayList<>();

    public Tttt() {
        setTitle("Cricket Player Stats Management System");
        setSize(900, 500);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        BackgroundPanel background = new BackgroundPanel("C://Users//Home//Desktop/20.png");
        background.setLayout(null);
        setContentPane(background);

        JLabel heading = new JLabel("(Players Stats)");
        heading.setFont(new Font("Arial", Font.BOLD, 32));
        heading.setHorizontalAlignment(SwingConstants.CENTER);
        heading.setVerticalAlignment(SwingConstants.CENTER);
        heading.setForeground(Color.white);
        heading.setBounds(230, 10, 300, 30);
        background.add(heading);

        String[] playerTypes = {"Select", "Batsman", "Bowler", "Allrounder"};
        typeBox = new JComboBox<>(playerTypes);
        addLabel(background, "Player Type:", 60);
        typeBox.setBounds(150, 60, 150, 25);
        background.add(typeBox);

        nameField = new JTextField();
        addLabel(background, "Name:", 100);
        nameField.setBounds(150, 100, 150, 25);
        nameField.setBackground(Color.black);
        nameField.setForeground(Color.white);
        nameField.setFont(new Font("Monospaced", Font.BOLD, 14));
        background.add(nameField);

        ageField = new JTextField();
        addLabel(background, "Age:", 140);
        ageField.setBounds(150, 140, 150, 25);
        ageField.setBackground(Color.black);
        ageField.setForeground(Color.white);
        ageField.setFont(new Font("Monospaced", Font.BOLD, 14));
        background.add(ageField);

        runsField = new JTextField();
        addLabel(background, "Runs:", 180);
        runsField.setBounds(150, 180, 150, 25);
        runsField.setBackground(Color.black);
        runsField.setForeground(Color.white);  
        runsField.setFont(new Font("Monospaced", Font.BOLD, 14));
        background.add(runsField);

        wicketsField = new JTextField();
        addLabel(background, "Wickets:", 220);
        wicketsField.setBounds(150, 220, 150, 25);
        wicketsField.setBackground(Color.black);
        wicketsField.setForeground(Color.white);
        background.add(wicketsField);

        matchesField = new JTextField();
        addLabel(background, "Matches:", 260);
        matchesField.setBounds(150, 260, 150, 25);
        matchesField.setBackground(Color.black);
        matchesField.setForeground(Color.white);
        matchesField.setFont(new Font("Monospaced", Font.BOLD, 14));
        background.add(matchesField);

        avgField = new JTextField();
        addLabel(background, "Bat Avg:", 300);
        avgField.setBounds(150, 300, 150, 25);
        avgField.setBackground(Color.black);
        avgField.setForeground(Color.white);
        avgField.setFont(new Font("Monospaced", Font.BOLD, 14));
        background.add(avgField);

        ecoField = new JTextField();
        addLabel(background, "Economy:", 340);
        ecoField.setBounds(150, 340, 150, 25);
        ecoField.setFont(new Font("Monospaced", Font.BOLD, 14));
        ecoField.setBackground(Color.black);
        ecoField.setForeground(Color.white);
        background.add(ecoField);

        JButton addButton = new JButton("Add Player");
        JButton showButton = new JButton("Show All Players");
        addButton.setBounds(150, 390, 130, 30);
        showButton.setBounds(300, 390, 180, 30);
        styleButton(addButton);
        styleButton(showButton);
        background.add(addButton);
        background.add(showButton);

        outputArea = new JTextArea();
        outputArea.setEditable(false);
        outputArea.setFont(new Font("Monospaced", Font.BOLD, 14));
        outputArea.setMargin(new Insets(10, 10, 10, 10));
        outputArea.setBackground(Color.black);
        outputArea.setForeground(Color.white);
        JScrollPane scrollPane = new JScrollPane(outputArea);
        scrollPane.setBounds(500, 60, 350, 300);
        background.add(scrollPane);

        addButton.addActionListener(e -> addPlayer());
        showButton.addActionListener(e -> showAllPlayers());

        setVisible(true);
    }

    private void styleButton(JButton button) {
        button.setForeground(Color.white);
        button.setBackground(Color.black);
        button.setOpaque(true);
        button.setBorderPainted(false);
    }

    private void addLabel(JComponent parent, String text, int y) {
        JLabel label = new JLabel(text);
        label.setBounds(50, y, 100, 25);
        label.setFont(new Font("Arial", Font.BOLD, 14));
        label.setForeground(Color.white);
        parent.add(label);
    }

    private void addPlayer() {
        try {
            String type = (String) typeBox.getSelectedItem();
            String name = nameField.getText();
            int age = Integer.parseInt(ageField.getText());

            if ("Batsman".equals(type)) {
                Batsman b = new Batsman();
                b.setType(type);
                b.setName(name);
                b.setAge(age);
                b.setBatsmanStats(
                        Integer.parseInt(runsField.getText()),
                        Integer.parseInt(matchesField.getText()),
                        Float.parseFloat(avgField.getText())
                );
                players.add(b);
            } else if ("Bowler".equals(type)) {
                Bowler b = new Bowler();
                b.setType(type);
                b.setName(name);
                b.setAge(age);
                b.setBowlerStats(
                        Integer.parseInt(wicketsField.getText()),
                        Integer.parseInt(matchesField.getText()),
                        Float.parseFloat(ecoField.getText())
                );
                players.add(b);
            } else if ("Allrounder".equals(type)) {
                Allrounder a = new Allrounder();
                a.setType(type);
                a.setName(name);
                a.setAge(age);
                a.setAllrounderStats(
                        Integer.parseInt(runsField.getText()),
                        Integer.parseInt(wicketsField.getText()),
                        Integer.parseInt(matchesField.getText()),
                        Float.parseFloat(avgField.getText()),
                        Float.parseFloat(ecoField.getText())
                );
                players.add(a);
            } else {
                JOptionPane.showMessageDialog(this, "Please select a valid player type.");
                return;
            }

            JOptionPane.showMessageDialog(this, "Player added successfully!");
            clearFields();
        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Please enter valid numeric values in all required fields.");
        }
    }

    private void clearFields() {
        nameField.setText("");
        ageField.setText("");
        runsField.setText("");
        wicketsField.setText("");
        matchesField.setText("");
        avgField.setText("");
        ecoField.setText("");
        typeBox.setSelectedIndex(0);
    }

    private void showAllPlayers() {
        if (players.isEmpty()) {
            outputArea.setText("No players added yet.");
            writeToFile("No players added yet.");
            return;
        }
        StringBuilder sb = new StringBuilder();
        for (Player p : players) {
            sb.append(centerText(p.getStats())).append("\n\n--------------------\n\n");
        }
        String output = sb.toString();
        outputArea.setText(output);
        writeToFile(output);
    }

    private String centerText(String input) {
        String[] lines = input.split("\n");
        StringBuilder centered = new StringBuilder();
        for (String line : lines) {
            int padding = (40 - line.length()) / 2;
            for (int i = 0; i < Math.max(0, padding); i++) centered.append(" ");
            centered.append(line).append("\n");
        }
        return centered.toString();
    }

    private void writeToFile(String content) {
        try (FileWriter writer = new FileWriter("player_stats.txt")) {
            writer.write(content);
        } catch (IOException e) {
            JOptionPane.showMessageDialog(this, "Error writing to file: " + e.getMessage());
        }
    }

    class BackgroundPanel extends JPanel {
        private final Image bgImage;

        public BackgroundPanel(String imagePath) {
            ImageIcon icon = new ImageIcon(imagePath);
            bgImage = icon.getImage();
        }

        @Override
        protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            g.drawImage(bgImage, 0, 0, getWidth(), getHeight(), this);
        }
    }

    public static void main(String[] args) {
         SwingUtilities.invokeLater(Tttt::new);
    }
}

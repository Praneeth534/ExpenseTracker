# ExpenseTracker
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.ArrayList;

public class ExpenseTracker {
    private JFrame frame;
    private DefaultListModel<String> expenseModel;
    private JList<String> expenseList;
    private ArrayList<Double> expenses;

    public ExpenseTracker() {
        expenses = new ArrayList<>();
        frame = new JFrame("Expense Tracker");
        expenseModel = new DefaultListModel<>();
        expenseList = new JList<>(expenseModel);
        JTextField descriptionField = new JTextField(20);
        JTextField amountField = new JTextField(10);
        JButton addButton = new JButton("Add Expense");

        addButton.addActionListener(e -> {
            String description = descriptionField.getText();
            String amountStr = amountField.getText();
            if (!description.isEmpty() && !amountStr.isEmpty()) {
                double amount = Double.parseDouble(amountStr);
                expenses.add(amount);
                expenseModel.addElement(description + ": $" + amount);
                descriptionField.setText("");
                amountField.setText("");
            }
        });

        JPanel panel = new JPanel();
        panel.add(new JLabel("Description:"));
        panel.add(descriptionField);
        panel.add(new JLabel("Amount:"));
        panel.add(amountField);
        panel.add(addButton);
        frame.add(panel, BorderLayout.NORTH);
        frame.add(new JScrollPane(expenseList), BorderLayout.CENTER);
        frame.setSize(300, 200);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(ExpenseTracker::new);
    }
}

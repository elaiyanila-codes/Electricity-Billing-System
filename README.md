# Electricity-Billing-System
import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class ElectricityBillingSystemSwing {

    // Method to calculate the electricity bill based on units consumed
    public static double calculateBill(double unitsConsumed) {
        double bill = 0;
        if (unitsConsumed <= 100) {
            bill = unitsConsumed * 5; // Rs. 5 per unit for the first 100 units
        } else if (unitsConsumed <= 200) {
            bill = 100 * 5 + (unitsConsumed - 100) * 7; // Rs. 7 per unit for 101-200 units
        } else if (unitsConsumed <= 300) {
            bill = 100 * 5 + 100 * 7 + (unitsConsumed - 200) * 10; // Rs. 10 per unit for 201-300 units
        } else {
            bill = 100 * 5 + 100 * 7 + 100 * 10 + (unitsConsumed - 300) * 12; // Rs. 12 per unit for above 300 units
        }
        return bill;
    }

    public static void main(String[] args) {
        // Create the main frame
        JFrame frame = new JFrame("Electricity Billing System");
        frame.setSize(400, 400);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        // Create panels for the layout
        JPanel panel = new JPanel();
        panel.setLayout(new GridLayout(8, 2, 10, 10));

        // Add components for input fields
        JLabel nameLabel = new JLabel("Customer Name:");
        JTextField nameField = new JTextField();

        JLabel idLabel = new JLabel("Customer ID:");
        JTextField idField = new JTextField();

        JLabel unitsLabel = new JLabel("Units Consumed:");
        JTextField unitsField = new JTextField();

        JButton calculateButton = new JButton("Calculate Bill");

        JLabel billLabel = new JLabel("Total Bill Amount (Rs):");
        JLabel billAmountLabel = new JLabel();

        JLabel gstLabel = new JLabel("GST (18%):");
        JLabel gstAmountLabel = new JLabel();

        JLabel totalLabel = new JLabel("Total with GST (Rs):");
        JLabel totalWithGstLabel = new JLabel();

        // Add components to the panel
        panel.add(nameLabel);
        panel.add(nameField);
        panel.add(idLabel);
        panel.add(idField);
        panel.add(unitsLabel);
        panel.add(unitsField);
        panel.add(calculateButton);
        panel.add(new JLabel()); // Empty cell
        panel.add(billLabel);
        panel.add(billAmountLabel);
        panel.add(gstLabel);
        panel.add(gstAmountLabel);
        panel.add(totalLabel);
        panel.add(totalWithGstLabel);

        // Add panel to frame
        frame.add(panel);

        // Button action listener to calculate the bill
        calculateButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    String customerName = nameField.getText();
                    String customerId = idField.getText();
                    double unitsConsumed = Double.parseDouble(unitsField.getText());

                    double billAmount = calculateBill(unitsConsumed);
                    double gst = billAmount * 0.18;
                    double totalWithGST = billAmount + gst;

                    billAmountLabel.setText(String.format("%.2f", billAmount));
                    gstAmountLabel.setText(String.format("%.2f", gst));
                    totalWithGstLabel.setText(String.format("%.2f", totalWithGST));

                } catch (NumberFormatException ex) {
                    JOptionPane.showMessageDialog(frame, "Please enter valid inputs.", "Error", JOptionPane.ERROR_MESSAGE);
                }
            }
        });

        // Set frame visibility
        frame.setVisible(true);
    }
}

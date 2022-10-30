# CHAT-APPLICATION
Source Code of Chat Application
SERVER CHAT

//Press Shift + F6 to run the program
package defenceyourchatapp;

import java.io.*;
import java.net.*;
import java.util.Scanner;
import javax.swing.*;

public class ServerChat extends javax.swing.JFrame {

    static ServerSocket serverSocket;
    static Socket socket;
    static DataInputStream dinStream;
    static DataOutputStream doutStream;

    public ServerChat() {
        initComponents();
    }

    @SuppressWarnings("unchecked")
    // <editor-fold defaultstate="collapsed" desc="Generated Code">                          
    private void initComponents() {

        jScrollPane1 = new javax.swing.JScrollPane();
        messageArea = new javax.swing.JTextArea();
        messageText = new javax.swing.JTextField();
        messageSend = new javax.swing.JButton();
        jLabel1 = new javax.swing.JLabel();
        exitButton = new javax.swing.JButton();
        jLabel2 = new javax.swing.JLabel();

        setDefaultCloseOperation(javax.swing.WindowConstants.EXIT_ON_CLOSE);
        getContentPane().setLayout(null);

        messageArea.setColumns(20);
        messageArea.setRows(5);
        jScrollPane1.setViewportView(messageArea);

        getContentPane().add(jScrollPane1);
        jScrollPane1.setBounds(6, 38, 391, 300);
        getContentPane().add(messageText);
        messageText.setBounds(6, 344, 391, 31);

        messageSend.setText("SEND");
        messageSend.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                messageSendActionPerformed(evt);
            }
        });
        getContentPane().add(messageSend);
        messageSend.setBounds(174, 381, 62, 28);

        jLabel1.setFont(new java.awt.Font("Tahoma", 1, 12)); // NOI18N
        jLabel1.setText("SERVER");
        getContentPane().add(jLabel1);
        jLabel1.setBounds(175, 13, 48, 15);

        exitButton.setBackground(new java.awt.Color(0, 153, 153));
        exitButton.setForeground(new java.awt.Color(153, 0, 0));
        exitButton.setText("EXIT");
        exitButton.setFocusable(false);
        exitButton.addActionListener(new java.awt.event.ActionListener() {
            public void actionPerformed(java.awt.event.ActionEvent evt) {
                exitButtonActionPerformed(evt);
            }
        });
        getContentPane().add(exitButton);
        exitButton.setBounds(344, 6, 53, 28);

        jLabel2.setIcon(new javax.swing.ImageIcon("C:\\Users\\Mikuuitou\\Downloads\\tree-of-life-4k-y5.jpg")); // NOI18N
        jLabel2.setText("jLabel2");
        getContentPane().add(jLabel2);
        jLabel2.setBounds(-4, 0, 410, 420);

        pack();
    }// </editor-fold>                        

    private void messageSendActionPerformed(java.awt.event.ActionEvent evt) {                                            
        // SEND BUTTON
        // TODO ADD YOUR HANDLING CODE HERE:

        try {
            String user = "Me";
            String message;
            message = messageText.getText();
            doutStream.writeUTF(message);
            messageText.setText("");
            messageArea.setText(messageArea.getText() + "\n" + user + ": " + message);

        } catch (Exception e) {
            //HANDLE THE EXCEPTION HERE
        }
    }                                           

    private void exitButtonActionPerformed(java.awt.event.ActionEvent evt) {                                           
        // EXIT BUTTON
        // TODO ADD YOUR HANDLING CODE HERE:

        JFrame frame = new JFrame("EXIT");
        if (JOptionPane.showConfirmDialog(frame, "Confirm if you want to Exit", "EXIT",
                JOptionPane.YES_NO_OPTION) == JOptionPane.YES_NO_OPTION) {
            System.exit(0);
        }

    }                                          

    public static void main(String args[]) {
        /* Set the Nimbus look and feel */
        //<editor-fold defaultstate="collapsed" desc=" Look and feel setting code (optional) ">
        //java.util.logging.Logger.getLogger(ServerChat.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        /* If Nimbus (introduced in Java SE 6) is not available, stay with the default look and feel.
         * For details see http://download.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html 
         */
        /*java.awt.EventQueue.invokeLater(new Runnable() {
         public void run() {
         new ServerChat().setVisible(true);
         }
         });*/

        try {
            for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
                if ("Nimbus".equals(info.getName())) {
                    javax.swing.UIManager.setLookAndFeel(info.getClassName());
                    break;
                }
            }
        } catch (ClassNotFoundException ex) {
            java.util.logging.Logger.getLogger(ServerChat.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (InstantiationException ex) {
            java.util.logging.Logger.getLogger(ServerChat.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (IllegalAccessException ex) {
            java.util.logging.Logger.getLogger(ServerChat.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        } catch (javax.swing.UnsupportedLookAndFeelException ex) {
            java.util.logging.Logger.getLogger(ServerChat.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
        }
        //</editor-fold>

        //USERNAME INPUT
        Scanner miku = new Scanner(System.in);
        String user;

        System.out.print("Enter a username for the client : ");
        user = miku.next();

        /* CREATE AND DISPLAY THE FORM */
        java.awt.EventQueue.invokeLater(new Runnable() {
            public void run() {
                new ServerChat().setVisible(true);
            }
        });

        try {
            String messageInput = "";
            serverSocket = new ServerSocket(1908);
            socket = serverSocket.accept();
            dinStream = new DataInputStream(socket.getInputStream());
            doutStream = new DataOutputStream(socket.getOutputStream());

            while (!messageInput.equals("EXIT")) {

                messageInput = dinStream.readUTF();
                messageArea.setText(messageArea.getText() + "\n" + user + ": " + messageInput);

            }

        } catch (Exception e) {

        }

    }

    // Variables declaration - do not modify                     
    private javax.swing.JButton exitButton;
    private javax.swing.JLabel jLabel1;
    private javax.swing.JLabel jLabel2;
    private javax.swing.JScrollPane jScrollPane1;
    private static javax.swing.JTextArea messageArea;
    private javax.swing.JButton messageSend;
    private javax.swing.JTextField messageText;
    // End of variables declaration                   
}

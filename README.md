# Javascript
Javascript practice 
/*
Pracs 6 - Swing
b) Create a Swing application to demonstrate use of TextArea using scrollpane to show contest of text file in textarea selected using file chooser.
*/

import javax.swing.*;
import javax.swing.filechooser.FileNameExtensionFilter;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.*;

public class P6b extends JFrame implements ActionListener 
{
    	private JTextArea textArea;
    	private JButton openButton;
    	private JFileChooser fileChooser;

    	public P6b() 
	{
		// Set the title of the JFrame
        	super("Swing - File Viewer App"); 
        
		// Set default close operation
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE); 
        
		// Set the size of the JFrame
		setSize(600, 400); 

        	// Create a JTextArea to display file contents
        	textArea = new JTextArea();

		 // Make it non-editable
        	textArea.setEditable(false);

		// Enable line wrapping
        	textArea.setLineWrap(true); 

		// Wrap at word boundaries
        	textArea.setWrapStyleWord(true); 

        	// Create a JScrollPane to hold the JTextArea
        	JScrollPane scrollPane = new JScrollPane(textArea);
        
		// Always show vertical scrollbar
		scrollPane.setVerticalScrollBarPolicy(JScrollPane.VERTICAL_SCROLLBAR_ALWAYS); 
       

		// Always show horizontal scrollbar										 		scrollPane.setHorizontalScrollBarPolicy(JScrollPane.HORIZONTAL_SCROLLBAR_ALWAYS); 

        	// Create a JButton to open the file chooser
        	openButton = new JButton("Open File");

		// Register ActionListener to the button
        	openButton.addActionListener(this); 

       		// Create a JFileChooser
        	fileChooser = new JFileChooser();
        
		// Allow only text files
		fileChooser.setFileFilter(new FileNameExtensionFilter("Text Files", "txt")); 

        	// Create a JPanel to hold the button
        	JPanel buttonPanel = new JPanel();
        	buttonPanel.add(openButton);

        	// Add components to the JFrame
        	getContentPane().setLayout(new BorderLayout());
        	getContentPane().add(scrollPane, BorderLayout.CENTER);
        	getContentPane().add(buttonPanel, BorderLayout.SOUTH);

        	// Make frame visible
        	setVisible(true); // Set the JFrame to be visible
    	}//P6b() 

    	// ActionListener implementation
    	@Override
    	public void actionPerformed(ActionEvent e) 
	{
        	if (e.getSource() == openButton) 
		{ 
			// Check if the open button is clicked
            		int returnVal = fileChooser.showOpenDialog(this); // Show the file chooser dialog

            		if (returnVal == JFileChooser.APPROVE_OPTION) 
			{ 
				// If a file is chosen
                		File file = fileChooser.getSelectedFile(); // Get the selected file

                		try 
				{
                    			// Read the contents of the file and display it in the text area
                    			BufferedReader reader = new BufferedReader(new FileReader(file));
                    			StringBuilder content = new StringBuilder();
                    			String line;
                    
					while ((line = reader.readLine()) != null) 
					{
                        			content.append(line).append("\n");
                    			}//while
                    			reader.close();
                    			textArea.setText(content.toString());
                		}//try	 
				catch (IOException ex) 
				{
                    			ex.printStackTrace();
                    			JOptionPane.showMessageDialog(this, "Error reading file: " + ex.getMessage(), "Error", JOptionPane.ERROR_MESSAGE);
                		}//catch()
            		}//if (returnVal ...)
        	}//f (e.getSource()...) 
   	 }//actionPerformed()

    	// Main method to start the application
    	public static void main(String[] args) 
	{
        	// Create and run the FileViewerApp
        	SwingUtilities.invokeLater(new Runnable() 
		{
            		@Override
            		public void run() 
			{
                		new P6b(); // Create an instance of FileViewerApp
            		}//run()
        	});//SwingUtilities.invokeLater()
    	}//main()
}//class P6b









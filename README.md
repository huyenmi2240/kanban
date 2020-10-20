# kanban
import java.awt.Color;
import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.util.function.Consumer;
import javax.swing.JPanel;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JButton;


public class Board extends JFrame implements ActionListener{
	
	JButton button = new JButton("Click to add task");
	JPanel panel = new JPanel();
	JLabel label = new JLabel();
	boolean check;
	int i;
	
	public Board() {
		setTitle("Kanban");
		setSize(960, 960); 
		setVisible(true);
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		
		button.addActionListener(this);
		panel.add(button);
		add(panel, "North");
		panel.add(button);
		panel.add(label);		
		check = false;
		
	}
	public void paint(Graphics g) {
		//ToDoColumn//
		g.setColor(Color.black);
		g.drawRect(50, 100, 250, 600);
		
		g.setColor(Color.lightGray);
		g.fillRect(75, 120, 200, 50);
		
		g.setColor(Color.black);
		g.drawString("To Do", 150, 150);
		
		//BeingDoneColumn//
		g.setColor(Color.BLACK);
		g.drawRect(350, 100, 250, 600);
		
		g.setColor(Color.lightGray);
		g.fillRect(375, 120, 200, 50);
		
		g.setColor(Color.black);
		g.drawString("Being Done", 440, 150);
		
		//DoneColumn//
		g.setColor(Color.BLACK);
		g.drawRect(650, 100, 250, 600);
		
		g.setColor(Color.lightGray);
		g.fillRect(675, 120, 200, 50);
		
		g.setColor(Color.black);
		g.drawString("Done", 760, 150);
		
	}
	public Consumer<? super String> paint2 (Graphics g) {
		g.setColor(Color.yellow);
		g.fillRect(90, 200, 75, 75);
		
		g.setColor(Color.black);
		int x;
		x=0;
		x++;
		g.drawString("Task" + x, 108, 243);
		return null;
	}
	public static void main(String[] args) {
		Task task1 = new Task();
		task1.populateData();
		
		
		Board b = new Board();// TODO Auto-generated method stub
		b.paint(null);
	}
	@Override
	public void actionPerformed (ActionEvent e) {
		paint2(getGraphics());
		}
	}
  
  /////////subclass "Task" below this line ////////////
  
  import java.util.ArrayList;
import java.util.Scanner;

public class Task extends Board{
	
	public String name;
	public String importance;
	public String duration;
	public String status;
	
	public String another;
	
	public ArrayList<String> taskList = new ArrayList();
	
	public void populateData() {	
		Scanner kbd_scanner = new Scanner(System.in);	
		
		status = "To Do";
		
		System.out.println("Please input task name: ");
		name = kbd_scanner.nextLine();
		
		taskList.add(name);
		
		System.out.println("Task importance: ");
		importance = kbd_scanner.nextLine();
		System.out.println("Task duration: ");
		duration = kbd_scanner.nextLine();
		System.out.println("Task status: " + status);
		
		System.out.println("Enter another task? Yes/No");
		another = kbd_scanner.nextLine();
		
		if(another == "No") {
			System.out.println(" ");
		}
		else {
			while(another.equals("Yes")){
	
				System.out.println("Please input task name: ");
				name = kbd_scanner.nextLine();	
				
				taskList.add(name);
				
				System.out.println("Task importance: ");
				importance = kbd_scanner.nextLine();
				System.out.println("Task duration: ");
				duration = kbd_scanner.nextLine();
				System.out.println("Task status: " + status);
		
				System.out.println("Enter another task? Yes/No");
				another = kbd_scanner.nextLine();
			}
		}
		System.out.println(taskList);
		taskList.forEach(paint2(getGraphics()));
	}
}

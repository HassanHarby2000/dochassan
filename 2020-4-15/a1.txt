
import javax.swing.JFrame;

import java.awt.Graphics;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

import javax.swing.*;
abstract class Person{
protected int id ;
protected String name ;
protected int age ;
public Person(int id, String name, int age){
this.id = id ;
this.name = name ;
this.age =age ;
}
public abstract void Person_Info();
}



// 
//
class Student extends Person  {
private double grade ;
public Student (int id, String name, int age,double grade){
super(id,name,age);
this.grade=grade;
}
@Override
public void Person_Info(){
System.out.println("id " + id );
System.out.println("name " + name );
System.out.println("age " + age );
System.out.println("grade  " + grade  );
}
}


class Teacher extends Person  {
private double salary ;
public Teacher (int id, String name, int age,double salary ){
super(id,name,age);
this.salary = salary ;
}
@Override
public void Person_Info(){
System.out.println("id " + id );
System.out.println("name " + name );
System.out.println("age " + age );
System.out.println("salary " + salary );
}
}


// panel
// -----------------------------------------
class panel extends JPanel implements ActionListener   {
 Person person;
  ButtonGroup group = new ButtonGroup();
  JRadioButton btn1 = new JRadioButton("teacher");
  JRadioButton btn2 = new JRadioButton("student "); 
  
  JLabel lab1 = new JLabel("ID"); 
  JLabel lab2 = new JLabel("Name");
  JLabel lab3 = new JLabel("Age");
  JLabel lab4 = new JLabel("" );
  JTextField textField1=new JTextField();;
  JTextField textField2=new JTextField();;
  JTextField textField3=new JTextField();;
  JTextField textField4=new JTextField();;
  JButton  b1 = new JButton("Add");
   public panel(){
      group.add(btn1 );
        group.add(btn2 ); 
        add(btn1);
        add(btn2);
        add(lab1);
        add(lab2);
        add(lab3);
        add(lab4);
        add(textField1);
        add(textField2);
        add(textField3);
        
        add(b1);
  btn1.setActionCommand("teacher");
  btn2.setActionCommand("student");
  btn1.addActionListener(this);
  btn2.addActionListener(this);

  b1.setActionCommand("add");
  b1.addActionListener(this);
} 
@Override
    protected void paintComponent(Graphics g) {
        super.paintComponent(g);

        //setSize
        textField1.setSize(100,20);
         textField2.setSize(100,20);
          textField3.setSize(100,20);
         textField4.setSize(100,20);
//pos
        btn1.setLocation(100,10);
         btn2.setLocation(100,30);
          lab1.setLocation(25,60);
         lab2.setLocation(25,80);
          lab3.setLocation(25,100);
         lab4.setLocation(25,120);
          textField1.setLocation(100,60);
         textField2.setLocation(100,80);
          textField3.setLocation(100,100);
         textField4.setLocation(100,120);
          b1.setLocation(100,150);
         

        
       
        

    }
   public void actionPerformed(ActionEvent e) {
    if ("add".equals(e.getActionCommand())) {
      if(lab4.getText()=="salary")  {
          if((int)Integer.parseInt(textField4.getText())<0) 
         JOptionPane.showMessageDialog(null, "salary can`t be negative","Error" ,JOptionPane.ERROR_MESSAGE); 
         else {
           try {
  person=new Teacher(
            (int) Integer.parseInt(textField1.getText())
             , textField2.getText()
             ,(int)Integer.parseInt(textField3.getText())
             ,(int)Integer.parseInt(textField4.getText())
             );
}
catch(Exception  e1) {
 
}
           
              JOptionPane.showMessageDialog(null, "New teacher added");
         }

      } else if(lab4.getText()=="grade"){
              if((int)Integer.parseInt(textField4.getText())<0) 
         JOptionPane.showMessageDialog(null, "grade can`t be negative","Error", JOptionPane.ERROR_MESSAGE); 
               else if((int)Integer.parseInt(textField4.getText())<100)
                JOptionPane.showMessageDialog(null, "grade can`t exceed 100","Error" , JOptionPane.ERROR_MESSAGE);
                   else {
                  try {
   person=new Student(
             (int)Integer.parseInt(textField1.getText())
             , textField2.getText()
             ,(int)Integer.parseInt(textField3.getText())
             ,(int)Integer.parseInt(textField4.getText())
             );
}
catch(Exception e1) {
 
}
         
              JOptionPane.showMessageDialog(null, "New student added");
         }

      }
    } else if ("teacher".equals(e.getActionCommand())) {
      lab4.setText("salary");
         add(textField4);
    } else if ("student".equals(e.getActionCommand())) {
        add(textField4);
      lab4.setText("grade");
    }}


}

// Main
// -----------------------------------------
class Main {
  public static void main(String[] args) {
    // System.out.println("Hello world!");
   JFrame from1= new JFrame("School`s Info");
   from1.add(new panel());
   from1.setSize(400, 400);

    from1.setVisible(true);
    

  }
}

import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.KeyEvent;
import java.awt.event.KeyListener;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.awt.event.MouseMotionListener;
import java.util.ArrayList;
import java.util.Random;
import java.awt.*;
import javax.swing.*;

/*
 * This project was created solo by me, Darnell Dail.
 * I call it Character Customize-inator V1.0. Since only I worked on it, everything you find here, I did.
 * 
 */
class Face {
	private String noseType = ("Normal");
	private String mouthType= ("Smile");
	private String eyeType = ("Medium");
	public String getNoseType() {
		return noseType;
	}
	public void setNoseType(String noseType) {
		this.noseType = noseType;
	}
	public String getMouthType() {
		return mouthType;
	}
	public void setMouthType(String mouthType) {
		this.mouthType = mouthType;
	}
	public String getEyeType() {
		return eyeType;
	}
	public void setEyeType(String eyeType) {
		this.eyeType = eyeType;
	}
	
	public Face (String mouthType, String noseType, String eyeType) {
		setNoseType(noseType);
		setEyeType(eyeType);
		setMouthType(mouthType);
	}
	
}

class FacePanel extends JPanel implements MouseListener,MouseMotionListener,
KeyListener {
	private Face avatar;
	@Override
	public void keyPressed(KeyEvent e) {}

	@Override
	public void keyReleased(KeyEvent e) {}

	@Override
	public void keyTyped(KeyEvent e) {}
	@Override
	public void mouseDragged(MouseEvent arg0) {}
	@Override
	public void mouseMoved(MouseEvent arg0) {}
	@Override
	public void mouseClicked(MouseEvent arg0) {}
	@Override
	public void mouseEntered(MouseEvent arg0) {}
	@Override
	public void mouseExited(MouseEvent arg0) {}
	@Override
	public void mousePressed(MouseEvent arg0) {}
	@Override
	public void mouseReleased(MouseEvent arg0) {}
	
	public FacePanel(Face avatar) {
		this.avatar = avatar;
	}
	
	@Override
	public void paintComponent(Graphics g) { // -------------------------------------------------- PAINT COMPONENT
		super.paintComponent(g);
		g.drawOval(125, 125, 300, 300);
		if (avatar.getEyeType().equals("Open")) { // Eye decider
			g.drawOval(175, 175, 50, 50);
			g.drawOval(310, 175, 50, 50);
		} else {
			g.drawLine(175, 200, 250, 200);
			g.drawLine(300, 200, 375, 200);
		}
		if (avatar.getNoseType().equals("Thick")) { // Nose decider
			g.drawOval(240, 250, 70, 50);
		} else {
			g.drawOval(260, 235, 30, 60);

		}
		if (avatar.getMouthType().equals("Smile")) { // Mouth decider
			g.drawArc(185, 275, 175, 125, 0, -180);
		} else if (avatar.getMouthType().equals("Frown")) {
			g.drawArc(200, 325, 150, 100, 0, 180);
		} else {
			g.drawLine(200, 350, 350, 350);
		}


	
	}
}
class FaceFrame extends JFrame implements ActionListener, KeyListener {
	private Face avatar;


	@Override
	public void paint(Graphics g) {
		super.paint(g);

	}
	public FaceFrame(Face avatar) {
		this.avatar = avatar;
		configureUI();
	}
	@Override
	public void actionPerformed(ActionEvent arg0) {}
	@Override
	public void keyPressed(KeyEvent arg0) {}
	@Override
	public void keyReleased(KeyEvent arg0) {}
	@Override
	public void keyTyped(KeyEvent arg0) {}
	
	public void configureMenu() {
		JMenuBar bar = new JMenuBar();
		JMenu mnuMouth = new JMenu("Mouth");
		JMenuItem miSmile = new JMenuItem("Smile");
		JMenuItem miFrown  = new JMenuItem("Frown");
		JMenuItem miNeutral = new JMenuItem("Neutral");
		mnuMouth.add(miSmile);
		mnuMouth.add(miFrown);
		mnuMouth.add(miNeutral);
		JMenu mnuNose = new JMenu("Nose");
		JMenuItem miThick = new JMenuItem("Thick");
		JMenuItem miSkinny = new JMenuItem("Skinny");
		mnuNose.add(miThick);
		mnuNose.add(miSkinny);
		JMenu mnuEyes = new JMenu("Eyes");
		JMenuItem miOpen = new JMenuItem("Open");
		JMenuItem miClosed  = new JMenuItem("Closed");
		mnuEyes.add(miOpen);
		mnuEyes.add(miClosed);
		miSmile.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				avatar.setMouthType("Smile");
				repaint();
			}
		});
		miFrown.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				avatar.setMouthType("Frown");
				repaint();
			}
		});		
		miNeutral.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				avatar.setMouthType("Neutral");
				repaint();
			}
		});		
		miThick.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				avatar.setNoseType("Thick");
				repaint();
			}
		});		
		miSkinny.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				avatar.setNoseType("Skinny");
				repaint();
			}
		});		
		miOpen.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				avatar.setEyeType("Open");
				repaint();
			}
		});		
		miClosed.addActionListener(new ActionListener() {
			public void actionPerformed(ActionEvent e) {
				avatar.setEyeType("Closed");
				repaint();
			}
		});
		bar.add(mnuMouth); // add an option to the actual menu bar
		bar.add(mnuNose); 
		bar.add(mnuEyes);
		setJMenuBar(bar);
	}
	
	public void configureUI() {
		setDefaultCloseOperation(EXIT_ON_CLOSE);
		setBounds(100,100,600,600);
		setTitle("Character Customization");
		Container c = getContentPane();
		c.setLayout(new BorderLayout());
		FacePanel fpan = new FacePanel(avatar);
		c.add(fpan,BorderLayout.CENTER);
		configureMenu();
	}
	
	
}



public class DailProject {
	public static void main(String[] args) {
		Face avatar = new Face("Neutral", "Skinny", "Open");
		FaceFrame ff = new FaceFrame(avatar);
		/*ff.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		ff.setTitle("Face Creator");
		ff.setBounds(100,100,600,600);*/
		ff.setVisible(true);

	}

}

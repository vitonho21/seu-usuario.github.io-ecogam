import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.Random;

public class EcoGame extends JFrame {

    private JLabel scoreLabel;
    private JLabel timeLabel;
    private JButton trashButton;
    private int score = 0;
    private int time = 30;
    private Random random = new Random();
    private Timer timer;

    public EcoGame() {

        setTitle("EcoGame - Limpe o Planeta");
        setSize(600,400);
        setLayout(null);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        JLabel title = new JLabel("Clique no lixo para limpar o meio ambiente 🌎");
        title.setBounds(150,10,350,30);
        add(title);

        scoreLabel = new JLabel("Pontuação: 0");
        scoreLabel.setBounds(20,40,120,30);
        add(scoreLabel);

        timeLabel = new JLabel("Tempo: 30");
        timeLabel.setBounds(500,40,100,30);
        add(timeLabel);

        trashButton = new JButton("🗑");
        trashButton.setFont(new Font("Arial",Font.PLAIN,30));
        trashButton.setBounds(200,150,80,60);
        add(trashButton);

        trashButton.addActionListener(new ActionListener(){
            public void actionPerformed(ActionEvent e){
                score++;
                scoreLabel.setText("Pontuação: " + score);
                moveTrash();
            }
        });

        startTimer();
        moveTrash();
    }

    private void moveTrash(){

        int x = random.nextInt(500);
        int y = random.nextInt(300);

        trashButton.setLocation(x,y);
    }

    private void startTimer(){

        timer = new Timer(1000,new ActionListener(){

            public void actionPerformed(ActionEvent e){

                time--;
                timeLabel.setText("Tempo: " + time);

                if(time <= 0){

                    timer.stop();

                    JOptionPane.showMessageDialog(null,
                            "Fim do jogo!\nPontuação: " + score +
                            "\nVocê ajudou a limpar o planeta!");

                }
            }
        });

        timer.start();
    }

    public static void main(String[] args){

        SwingUtilities.invokeLater(new Runnable(){
            public void run(){
                new EcoGame().setVisible(true);
            }
        });
    }
}

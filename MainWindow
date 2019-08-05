import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.MouseEvent;
import java.awt.event.MouseListener;
import java.util.Vector;

public class MainWindow extends JFrame {
    private int rows = 10;
    private int cols = 10;
    private int sizeW;
    private int sizeH;
    private Moving moving = new Moving(rows, cols);
    private JPanel mainPanel;
    private JPanel panelField;
    private JPanel panelControl;
    private JPanel panelSize;
    private JPanel panelExplanation;
    private Font font = new Font("Arial",Font.PLAIN, 17);
    private JButton runButton;

    private JRadioButton radioStart;
    private JRadioButton radioFinish;
    private JRadioButton radioBomb;
    private JTextField sizeFieldX;
    private JTextField sizeFieldY;


    MainWindow(){
        initMainWindow();
        initPanelControl();
        initPanel();
    }
    private void initMainWindow(){
        setTitle("Найти путь");
        setVisible(true);
        setSize(800, 800);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        mainPanel = new JPanel();
        mainPanel.setLayout(new BorderLayout());
        getContentPane().add(mainPanel);
    }
    private void initPanelControl(){
        panelControl = new JPanel();
        GridLayout layout = new GridLayout(3, 0, 5, 0);
        panelControl.setLayout(layout);
        initRadioButton();
        initPanelSize();
        initPanelExplanation();
        mainPanel.add(panelControl,BorderLayout.WEST);
    }
    private void initPanelSize(){

        JLabel labelWidth = new JLabel("Длина");
        JLabel labelHeight = new JLabel("Высота");

        labelWidth.setFont(font);
        labelHeight.setFont(font);
        panelSize = new JPanel();
        sizeFieldX = new JTextField("10", 3);
        sizeFieldY =new JTextField("10", 3);
        panelSize.setLayout(new GridLayout(6,1,2,0));

        panelSize.add(labelWidth);
        panelSize.add(sizeFieldX);
        panelSize.add(labelHeight);
        panelSize.add(sizeFieldY);
        initButton();
        panelControl.add(panelSize);
    }
    private void initPanelExplanation(){
        panelExplanation = new JPanel(){
            @Override
            protected void paintComponent(Graphics g) {
            super.paintComponent(g);
            Graphics2D g2 = (Graphics2D)g;
            g2.setColor(new Color(0xD6B8F2));
            g2.drawRect(0,0,(int)panelExplanation.getSize().getWidth(),160);
            g2.setColor(new Color(0x192134));
            g2.drawString("Пояснение",20,30);
            g2.setColor(new Color(0x85943C));
            g2.fillRect(10,50, 20,20);
            g2.setColor(new Color(0x4A6EA4));
            g2.fillRect(10,75, 20,20);
            g2.setColor(new Color(0xB70100));
            g2.fillRect(10,100, 20,20);
            g2.setColor(new Color(0x192134));
            g2.fillRect(10,125, 20,20);
            g2.drawString(" - Старт", 35,68);
            g2.drawString(" - Финиш", 35,93);
            g2.drawString(" - Бомба", 35,117);
            g2.drawString(" - Маршрут", 35,143);
            }
        };
        panelControl.add(panelExplanation);

    }

    private void initRadioButton(){
        ButtonGroup buttonGroup = new ButtonGroup();
        Box box = Box.createVerticalBox();
        //box.setLocation(1,50);
        JLabel l1 = new JLabel("Выберите объект");
        radioStart = new JRadioButton("Старт");
        radioFinish = new JRadioButton("Финиш");
        radioBomb = new JRadioButton("Бомба");
        radioBomb.setSelected(true);
        radioStart.setFont(font);
        radioFinish.setFont(font);
        radioBomb.setFont(font);
        buttonGroup.add(radioStart);
        buttonGroup.add(radioFinish);
        buttonGroup.add(radioBomb);
        l1.setFont(font);
        box.add(l1);
        box.add(radioStart);
        box.add(radioFinish);
        box.add(radioBomb);
        panelControl.add(box);
    }

    private  void initButton(){
        runButton = new JButton("Изменить");
        runButton.setFont(font);
        runButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                try {
                    rows = Integer.valueOf(sizeFieldX.getText());
                } catch (NumberFormatException i){
                    sizeFieldX.setText("10");
                }
                try {
                    cols = Integer.valueOf(sizeFieldY.getText());
                } catch (NumberFormatException i){
                    sizeFieldY.setText("10");
                }
                if(rows < 1){
                    rows = 10;
                    sizeFieldX.setText("10");
                }
                if(cols < 1){
                    cols = 10;
                    sizeFieldY.setText("10");
                }
                moving = new Moving(rows, cols);
                panelField.repaint();
            }

        });
        panelSize.add(runButton);
    }

    private void initPanel(){
        panelField = new JPanel(){
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                Graphics2D g2 = (Graphics2D) g;
                Vector<Point> path = moving.getPath();
                int[][] field = moving.getField();
                sizeW = getWidth() / rows;
                sizeH = getHeight() / cols;

                //рисуем поле
                for (int j = 0; j < sizeH * cols; j = j + sizeH) {
                    for (int i = 0; i < sizeW * rows; i = i + sizeW) {
                        g2.drawRect(i, j, sizeW, sizeH);
                    }
                }

                //рисуем старт
                g2.setColor(new Color(0x85943C));
                g2.fillRect(moving.getStartX()* sizeW + 1, moving.getStartY() * sizeH + 1, sizeW-1, sizeH-1);


                //рисуем финиш
                g2.setColor(new Color(0x4A6EA4));
                g2.fillRect(moving.getFinishX()* sizeW + 1, moving.getFinishY() * sizeH + 1, sizeW-1, sizeH-1);

                //рисуем бомбы
                g2.setColor(new Color(0xB70100));
                for (int x = 0; x < rows; x++) {
                    for (int y = 0; y < cols; y++) {
                        if(field[x][y] == Moving.BOMB){
                            g2.fillRect(x * sizeW + 1, y * sizeH + 1, sizeW-1, sizeH-1);
                        }
                    }
                }

                //рисуем путь
                g2.setColor(new Color(0x192134));
                for (Point m : path) {
                    g2.fillRect(((int) m.getX() )* sizeW + 1, (int) m.getY() * sizeH+ 1, sizeW-1, sizeH-1);
                }

            }
        };

        panelField.addMouseListener(new MouseListener() {
            @Override
            public void mouseClicked(MouseEvent e) {
                if(e.getX() / sizeW < rows && e.getY()/sizeH < cols){
                    if(radioBomb.isSelected()){
                        moving.addBomb(e.getX()/sizeW,e.getY()/sizeH);
                    }
                    if(radioStart.isSelected()){
                        moving.setStart(e.getX()/sizeW,e.getY()/sizeH);
                    }
                    if(radioFinish.isSelected()){
                        moving.setFinish(e.getX()/sizeW,e.getY()/sizeH);
                    }
                    panelField.repaint();
                }
            }

            @Override
            public void mousePressed(MouseEvent e) {

            }

            @Override
            public void mouseReleased(MouseEvent e) {

            }

            @Override
            public void mouseEntered(MouseEvent e) {

            }

            @Override
            public void mouseExited(MouseEvent e) {

            }
        });
        mainPanel.add(panelField, BorderLayout.CENTER);
    }
}

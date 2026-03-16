import java.awt.*;
import java.awt.event.*;
import java.awt.image.BufferedImage;
import java.io.BufferedInputStream;
import java.util.Random;
import javax.sound.sampled.AudioSystem;
import javax.sound.sampled.Clip;
import javax.swing.*;

class Key_actions implements KeyListener {

    public void keyTyped(KeyEvent k) {
        BouncingBall.c_code += k.getKeyChar();
        if (BouncingBall.c_code.length() == 10) {
            if (BouncingBall.c_code.toUpperCase().equals("PAINKILLER")) {
                BouncingBall.c_code = "";
                BouncingBall.level = 6;
            }
        } else if (BouncingBall.c_code.length() == 8) {
            if (BouncingBall.c_code.toUpperCase().equals("INFINITY")) {
                BouncingBall.Bullet_count = Integer.MAX_VALUE;
            }
        } else if (BouncingBall.c_code.length() > 10) {
            BouncingBall.c_code = "";
        }
    }

    public void keyPressed(KeyEvent kx) {
        if (kx.getKeyCode() == KeyEvent.VK_SPACE) {
            if (!BouncingBall.bullet_fire && !BouncingBall.won) {
                if (BouncingBall.startup_screen)
                    BouncingBall.startup_screen = false;
                BouncingBall.Bullet_count--;
                if (BouncingBall.Bullet_count < 0) {
                    BouncingBall.Bullet_count = 0;
                    BouncingBall.game_over.setVisible(true);
                } else {
                    BouncingBall.bullet_fire = true;
                    BouncingBall.c_code = "";
                    BouncingBall.Bullet_remaining.setText("Bales: " + BouncingBall.Bullet_count);
                    BouncingBall.show_popup = false;
                    BouncingBall.playSfx("/res/gunshot.wav");
                }
            } else if (BouncingBall.won) {
                BouncingBall.winner.setVisible(true);
            }
        }
    }

    public void keyReleased(KeyEvent key) {
    }
}

class Listener extends MouseAdapter {
    public void mouseClicked(MouseEvent e) {
        if (!BouncingBall.bullet_fire && !BouncingBall.won) {
            if (BouncingBall.startup_screen)
                BouncingBall.startup_screen = false;
            BouncingBall.Bullet_count--;
            if (BouncingBall.Bullet_count < 0) {
                BouncingBall.Bullet_count = 0;
                BouncingBall.game_over.setVisible(true);
            } else {
                BouncingBall.bullet_fire = true;
                BouncingBall.c_code = "";
                BouncingBall.Bullet_remaining.setText("Bales: " + BouncingBall.Bullet_count);
                BouncingBall.show_popup = false;
                BouncingBall.playSfx("/res/gunshot.wav");
            }
        } else if (BouncingBall.won) {
            BouncingBall.winner.setVisible(true);
        }
    }
}

class Button_Handler implements ActionListener {

    public static JCheckBox c1, c2;
    public static Boolean selected_BG = true;
    public static Boolean selected_GM = true;
    public static JFrame jf2;

    public void actionPerformed(ActionEvent e) {

        if (e.getActionCommand().equals("Guardar")) {
            if (c1.isSelected()) {
                BouncingBall.clip.stop();
                BouncingBall.clip.start();
                BouncingBall.bgmusic = true;
                selected_BG = true;
            } else {
                BouncingBall.clip.stop();
                BouncingBall.bgmusic = false;
                selected_BG = false;
            }
            BouncingBall.gamemusic = c2.isSelected();
            selected_GM = c2.isSelected();
            jf2.dispose();
        }

        if (e.getActionCommand().equals("Configuracio")) {
            jf2 = new JFrame("Configuracio");
            jf2.setLayout(null);
            JLabel l1 = new JLabel("Configuracio de so");
            JLabel l2 = new JLabel("Fet  per: CIDE");
            jf2.add(l1);
            jf2.add(l2);
            c1 = new JCheckBox("So de fons");
            c1.setSelected(selected_BG);
            c1.setBounds(80, 60, 150, 20);
            c1.setBackground(Color.WHITE);
            jf2.add(c1);
            c2 = new JCheckBox("Musica del joc");
            c2.setSelected(selected_GM);
            c2.setBounds(80, 90, 150, 20);
            c2.setBackground(Color.WHITE);
            jf2.add(c2);
            JButton save = new JButton("Guardar");
            save.addActionListener(new Button_Handler());
            save.setBackground(Color.WHITE);
            save.setBounds(100, 125, 100, 30);
            jf2.add(save);
            l1.setBounds(110, 30, 150, 20);
            l2.setBounds(160, 165, 130, 20);
            jf2.getContentPane().setBackground(Color.WHITE);
            jf2.setSize(300, 230);
            jf2.setResizable(false);
            jf2.setLocationRelativeTo(BouncingBall.framegame);
            jf2.setVisible(true);
        }

        if (e.getActionCommand().equals("Començar de nou")) {
            BouncingBall.Bullet_count = 6;
            BouncingBall.point = 0;
            BouncingBall.ball_speed = 8;
            BouncingBall.target = 20;
            BouncingBall.level = 1;
            BouncingBall.score.setText("Punts: 0");
            BouncingBall.Bullet_remaining.setText("Bales: 6");
            BouncingBall.Next_target.setText("Objectiu: 20");
            BouncingBall.Level.setText("Nivell: 1");
            BouncingBall.game_over.setVisible(false);
            BouncingBall.winner.setVisible(false);
            BouncingBall.move_ball = true;
            BouncingBall.bullet_fire = false;
            BouncingBall.ballx_base = 450;
            BouncingBall.bally_base = 400;
            BouncingBall.won = false;
            if (BouncingBall.bgmusic) {
                try {
                    BufferedInputStream af = new BufferedInputStream(
                            BouncingBall.bBall.getResourceAsStream("/res/theme.wav"));
                    BouncingBall.clip = AudioSystem.getClip();
                    BouncingBall.clip.open(AudioSystem.getAudioInputStream(af));
                    BouncingBall.clip.start();
                    BouncingBall.clip.loop(Clip.LOOP_CONTINUOUSLY);
                } catch (Exception ex) {
                    ex.printStackTrace();
                }
            }
        }

        if (e.getActionCommand().equals("Sortir")) {
            System.exit(0);
        }
    }
}

public class BouncingBall extends Canvas {

    // Resolucion de diseno base sobre la que estan definidas todas las coordenadas
    public static final int BASE_W = 800;
    public static final int BASE_H = 600;

    // Factores de escala actualizados en cada frame
    public static double scaleX = 1.0;
    public static double scaleY = 1.0;

    // Oscilacion vertical de la pelota (0-330 en espacio base)
    private static int x = 0;
    // Avance horizontal de la bala (0-700 en espacio base)
    private static int a = 0;
    public static boolean up = true;

    public static boolean move_ball = true;
    // Posicion de la pelota en espacio BASE
    public static int ballx_base = 450;
    public static int bally_base = 400;
    // Posicion de la bala en espacio BASE
    public static int bulletx_base = 20;
    public static int bullety_base = 278; // altura fija de disparo
    public static boolean bullet_fire = false;
    public static boolean bulletf = true;

    // Puntuacion y niveles
    public static int point = 0;
    public static boolean score_update = true;
    public static int target = 20;
    public static int level = 1;
    public static int ball_speed = 8; // ms por frame (menor = mas rapido)

    // Posiciones escaladas para dibujo (calculadas en animate)
    public static int ballx = 450;
    public static int bally = 400;
    public static int bulletx = 20;
    public static int bullety = 278;

    // Componentes de la interfaz
    public static JLabel score, gun, Bullet_remaining, Next_target, Level;
    public static Image img, gun_img, bullet_img, ball_img, img2;
    public static BufferedImage bf;
    public static JPanel detail_panel, bottom_buttons1, bottom_buttons2;
    public static Integer Bullet_count = 6;
    public static JDialog game_over, winner;
    public static JLabel game_over_msg, winning_msg;
    public static JButton restart, exit, restart2, exit2;

    // Racha y popups
    public static boolean level_changed = false;
    public static int consecutive_hit = 0;
    public static Font pop_font = new Font("Fugaz one", Font.PLAIN, 22);
    public static String popup_msg = "default";
    public static Boolean show_popup = false;
    public static Boolean hit = false;

    // Audio
    public static Clip clip;
    public static Boolean bgmusic = true;
    public static Boolean gamemusic = true;

    // Estado general
    public static Boolean startup_screen = true;
    public static Boolean won = false;
    public static Class bBall;
    public static JFrame framegame;
    public static String c_code = "";

    // Metodo auxiliar para reproducir efectos de sonido sin repetir codigo
    public static void playSfx(String resource) {
        if (!gamemusic)
            return;
        try {
            BufferedInputStream af = new BufferedInputStream(bBall.getResourceAsStream(resource));
            Clip hclip = AudioSystem.getClip();
            hclip.open(AudioSystem.getAudioInputStream(af));
            hclip.start();
        } catch (Exception ex) {
            ex.printStackTrace();
        }
    }

    public static void main(String[] args) {

        framegame = new JFrame("El mico disparador");
        framegame.setVisible(false);

        // Pantalla de inicio
        JFrame frame = new JFrame("Pantalla d'inici");
        frame.setSize(600, 450);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setResizable(false);
        frame.setLocationRelativeTo(null);

        JPanel panel = new JPanel(new GridBagLayout()) {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                Image bg = Toolkit.getDefaultToolkit().getImage(
                    BouncingBall.class.getResource("/res/fondo_cide2.png"));
                g.drawImage(bg, 0, 0, getWidth(), getHeight(), this);
            }
        };
        panel.setOpaque(false);
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(10, 10, 10, 10);
        gbc.fill = GridBagConstraints.HORIZONTAL;

        JLabel titulo = new JLabel("El mico disparador", JLabel.CENTER);
        titulo.setFont(new Font("Comic Sans MS", Font.BOLD, 40));
        titulo.setForeground(Color.WHITE);

        JButton reglas = new JButton("Com jugar");
        reglas.setFont(new Font("Comic Sans MS", Font.BOLD, 20));
        reglas.setBackground(Color.WHITE);
        reglas.addActionListener(l -> JOptionPane.showMessageDialog(frame,
                "Fes clic o prem ESPAI per disparar una bala.\n" +
                        "Cada cop dona 10 punts i colpejar al centre suma 20 punts.\n" +
                        "Recompensa d'1 bala extra per 2 cops consecutius.\n" +
                        "En arribar a la puntuacio objectiu, el nivell canvia.\n\n"));

        JButton begin = new JButton("Començar");
        begin.setFont(new Font("Comic Sans MS", Font.BOLD, 20));
        begin.setBackground(Color.WHITE);
        begin.addActionListener(ev -> {
            frame.dispose();
            framegame.setVisible(true);
        });

        gbc.gridx = 0;
        gbc.gridy = 0;
        gbc.gridwidth = 2;
        panel.add(titulo, gbc);
        gbc.gridy = 1;
        panel.add(begin, gbc);
        gbc.gridy = 2;
        panel.add(reglas, gbc);
        frame.add(panel);
        frame.setVisible(true);

        BouncingBall bouncingBall = new BouncingBall();
        bBall = bouncingBall.getClass();

        // Musica de fondo en bucle
        if (bgmusic) {
            try {
                BufferedInputStream af = new BufferedInputStream(bBall.getResourceAsStream("/res/theme.wav"));
                clip = AudioSystem.getClip();
                clip.open(AudioSystem.getAudioInputStream(af));
                clip.start();
                clip.loop(Clip.LOOP_CONTINUOUSLY);
            } catch (Exception ex) {
                ex.printStackTrace();
            }
        }

        // Barra de menu
        JMenuBar jmb = new JMenuBar();
        JMenuItem settings = new JMenuItem("Configuracio");
        jmb.add(settings);
        settings.setBackground(Color.WHITE);
        jmb.setBackground(Color.WHITE);
        framegame.setJMenuBar(jmb);

        Button_Handler bh = new Button_Handler();
        settings.addActionListener(bh);

        score = new JLabel("Punts: 0");
        Bullet_remaining = new JLabel("Bales: 6");
        Next_target = new JLabel("Objectiu: 20");
        Level = new JLabel("Nivell: 1");

        game_over = new JDialog(framegame, "Has perdut!");
        Image gOverImg = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/gameover_img.png"));
        JLabel gOverLbl = new JLabel(new ImageIcon(gOverImg.getScaledInstance(150, 150, Image.SCALE_DEFAULT)),
                SwingConstants.CENTER);
        game_over.getContentPane().setBackground(Color.WHITE);
        game_over.add(gOverLbl);
        bottom_buttons1 = new JPanel();
        bottom_buttons1.setBackground(Color.WHITE);
        restart = new JButton("Començar de nou");
        exit = new JButton("Sortir");
        restart.setBackground(Color.WHITE);
        exit.setBackground(Color.WHITE);
        restart.addActionListener(bh);
        exit.addActionListener(bh);
        bottom_buttons1.add(restart);
        bottom_buttons1.add(exit);
        game_over.add(bottom_buttons1, BorderLayout.SOUTH);
        game_over.setSize(300, 230);
        game_over.setResizable(false);

        winner = new JDialog(framegame, "Has guanyat!");
        Image wImg = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/winner_img.jpg"));
        JLabel wLbl = new JLabel(new ImageIcon(wImg.getScaledInstance(300, 350, Image.SCALE_DEFAULT)),
                SwingConstants.CENTER);
        winner.getContentPane().setBackground(Color.WHITE);
        winner.add(wLbl);
        bottom_buttons2 = new JPanel();
        restart2 = new JButton("Començar de nou");
        exit2 = new JButton("Sortir");
        restart2.setBackground(Color.WHITE);
        exit2.setBackground(Color.WHITE);
        restart2.addActionListener(bh);
        exit2.addActionListener(bh);
        bottom_buttons2.add(restart2);
        bottom_buttons2.add(exit2);
        winner.add(bottom_buttons2, BorderLayout.SOUTH);
        winner.setSize(300, 450);
        winner.setResizable(false);

        gun_img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/diddy_gun.png"));
        bullet_img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/bullet.png"));
        ball_img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/ball.png"));
        img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/fondo_cide.jpg"));
        img2 = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/fondo_cide2.png"));


        Canvas c = new BouncingBall();
        c.setFocusable(true);
        c.addKeyListener(new Key_actions());
        c.addMouseListener(new Listener());

        framegame.setLayout(new BorderLayout());
        framegame.add(c, BorderLayout.CENTER);

        framegame.setUndecorated(true);
        framegame.setExtendedState(JFrame.MAXIMIZED_BOTH);
        framegame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        framegame.setLocationRelativeTo(null);
        framegame.getContentPane().setBackground(new Color(34, 177, 76));
    }

    public BouncingBall() {
        Thread t = new Thread(() -> {
            while (true) {
                if (move_ball) {
                    // Comprueba victoria (nivel > 5)
                    if (level > 5 && !won) {
                        move_ball = false;
                        bullet_fire = false;
                        clip.stop();
                        if (bgmusic) {
                            try {
                                BufferedInputStream af = new BufferedInputStream(
                                        bBall.getResourceAsStream("/res/win.wav"));
                                Clip hclip = AudioSystem.getClip();
                                hclip.open(AudioSystem.getAudioInputStream(af));
                                hclip.start();
                            } catch (Exception ex) {
                                ex.printStackTrace();
                            }
                        }
                        won = true;
                        popup_msg = "GUANYADOR!";
                        Level.setText("Nivell: 5");
                        winner.setVisible(true);
                    }

                    // Oscila x entre 0 y 330 (rango de movimiento vertical)
                    if (up) {
                        x++;
                        if (x == 330)
                            up = false;
                    } else {
                        x--;
                        if (x == 0)
                            up = true;
                    }
                }
                try {
                    Thread.sleep(ball_speed);
                } catch (Exception e) {
                }
                repaint();
            }
        });
        t.start();

        Thread bullet = new Thread(() -> {
            while (bulletf) {

                if (point >= target && bullet_fire) {
                    level++;
                    level_changed = true;
                    Random rand = new Random();
                    int rv = rand.nextInt(10) + 40;
                    int dir = rand.nextInt(2) + 1;
                    if (dir == 1) {
                        ballx_base = (ballx_base + rv > 780) ? ballx_base - rv : ballx_base + rv;
                    } else {
                        ballx_base = (ballx_base - rv < 250) ? ballx_base + rv : ballx_base - rv;
                    }
                }

                if (a < 700 && bullet_fire) {
                    a += 5;
                    bulletx_base = a + 230;

                    int bPoint = bulletx_base + 38; // punta de la bala
                    int bOuter = ballx_base; // borde izquierdo de la pelota

                    if (bPoint == bOuter || (bPoint < bOuter + 10 && bPoint > bOuter - 10)) {

                        // Bono por racha de 2 impactos consecutivos -> bala extra
                        if (consecutive_hit == 2) {
                            playSfx("/res/bonus.wav");
                            popup_msg = "Bala +1";
                            show_popup = true;
                            consecutive_hit = 0;
                            Bullet_count++;
                            Bullet_remaining.setText("Bales: " + Bullet_count);
                        }

                        // Impacto en el CENTRO exacto -> 20 puntos
                        if (bullety_base - 15 == bally_base) {
                            if (score_update) {
                                score_update = false;
                                point += 20;
                                if (hit)
                                    consecutive_hit++;
                                if (Bullet_count > 0)
                                    move_ball = false;
                                hit = true;
                                ball_img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/explode.png"));
                                playSfx("/res/hit.wav");
                            }
                            score.setText("Punts: " + point);

                            // Zona central-baja -> 10 puntos
                        } else if (bally_base <= bullety_base && bally_base >= bullety_base - 19) {
                            if (score_update) {
                                score_update = false;
                                point += 15;
                                if (hit)
                                    consecutive_hit++;
                                if (Bullet_count > 0)
                                    move_ball = false;
                                hit = true;
                                ball_img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/explode.png"));
                                playSfx("/res/hit.wav");
                            }
                            score.setText("Punts: " + point);

                            // Zona superior -> 10 puntos
                        } else if (bally_base <= bullety_base - 21 && bally_base >= bullety_base - 35) {
                            if (score_update) {
                                score_update = false;
                                point += 15;
                                if (hit)
                                    consecutive_hit++;
                                if (Bullet_count > 0)
                                    move_ball = false;
                                hit = true;
                                ball_img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/explode.png"));
                                playSfx("/res/hit.wav");
                            }
                            score.setText("Punts: " + point);

                        } else {
                            hit = false;
                        }
                    }

                } else {
                    // Bala fuera de rango: reinicia estado
                    ball_img = Toolkit.getDefaultToolkit().getImage(bBall.getResource("/res/ball.png"));
                    score_update = true;
                    bullet_fire = false;
                    a = 0;

                    // Sin balas y sin alcanzar objetivo: Game Over
                    if (Bullet_count <= 0 && point < target) {
                        clip.stop();
                        if (move_ball) {
                            move_ball = false;
                            game_over.setVisible(true);
                            if (bgmusic) {
                                try {
                                    BufferedInputStream af = new BufferedInputStream(
                                            bBall.getResourceAsStream("/res/gameover.wav"));
                                    Clip hclip = AudioSystem.getClip();
                                    hclip.open(AudioSystem.getAudioInputStream(af));
                                    hclip.start();
                                } catch (Exception ex) {
                                    ex.printStackTrace();
                                }
                            }
                        }
                    } else {
                        move_ball = true;
                    }
                }

                if (level_changed) {
                    consecutive_hit = 0;
                    popup_msg = "Nivell: " + level;
                    show_popup = true;
                    if (level == 2) {
                        ball_speed -= 1;
                        Bullet_count = 6;
                        target += 30;
                    } else if (level == 3) {
                        ball_speed -= 1;
                        Bullet_count = 6;
                        target += 30;
                    } else if (level == 4) {
                        ball_speed -= 2;
                        Bullet_count = 5;
                        target += 30;
                    } else if (level == 5) {
                        ball_speed = 3;
                        Bullet_count = 5;
                        target += 30;
                    }
                    score.setText("Punts: " + point);
                    Level.setText("Nivell: " + level);
                    Next_target.setText("Objectiu: " + target);
                    Bullet_remaining.setText("Bales: " + Bullet_count);
                    level_changed = false;
                }

                try {
                    Thread.sleep(3);
                } catch (Exception e) {
                }
                repaint();
            }
        });
        bullet.start();
    }

    public void update(Graphics g) {
        paint(g);
    }

    public void paint(Graphics g) {
        int w = this.getWidth();
        int h = this.getHeight();
        if (w <= 0 || h <= 0)
            return;
        bf = new BufferedImage(w, h, BufferedImage.TYPE_INT_RGB);
        try {
            animate(bf.getGraphics(), w, h);
            g.drawImage(bf, 0, 0, null);
        } catch (Exception e) {
        }
    }

    public void animate(Graphics g, int W, int H) {
        super.paint(g);

        scaleX = (double) W / BASE_W;
        scaleY = (double) H / BASE_H;

        g.drawImage(img, 0, 0, W, H, this);

        g.drawImage(gun_img,
                (int) (-80 * scaleX), (int) (141 * scaleY),
                (int) (380 * scaleX), (int) (420 * scaleY), this);

        bally_base = 400 - x; // oscilacion vertical en base
        ballx = (int) (ballx_base * scaleX);
        bally = (int) (bally_base * scaleY);
        g.drawImage(ball_img, ballx, bally,
                (int) (50 * scaleX), (int) (50 * scaleY), this);

        if (bullet_fire) {
            bulletx_base = a + 230;
            bullety_base = 278;
            bulletx = (int) (bulletx_base * scaleX);
            bullety = (int) (bullety_base * scaleY);
            g.drawImage(bullet_img, bulletx, bullety,
                    (int) (30 * scaleX), Math.max(3, (int) (5 * scaleY)), this);
        }

        int hm = (int) (20 * scaleX); // margen lateral
        int hudH = (int) (60 * scaleY); // alto del HUD
        int hudY = (int) (10 * scaleY); // separacion superior
        int hudW = W - hm * 2; // ancho total menos margenes
        g.setColor(Color.WHITE);
        g.fillRoundRect(hm, hudY, hudW, hudH, 20, 30);

        // Textos del HUD distribuidos en 4 columnas equidistantes
        int fontSize = Math.max(12, (int) (17 * Math.min(scaleX, scaleY)));
        Font hudFont = new Font("Fugaz one", Font.PLAIN, fontSize);
        g.setFont(hudFont);
        g.setColor(Color.BLACK);
        FontMetrics fm = g.getFontMetrics(hudFont);
        int textY = hudY + (hudH + fm.getAscent() - fm.getDescent()) / 2;

        g.drawString("Bales: " + Bullet_count, hm + (int) (10 * scaleX), textY);
        g.drawString("Punts: " + point, hm + hudW / 4, textY);
        g.drawString("Objectiu: " + target, hm + hudW / 2, textY);
        g.drawString("Nivell: " + level, hm + 3 * hudW / 4, textY);

        if (show_popup) {
            int popW = (int) (160 * scaleX);
            int popH = (int) (50 * scaleY);
            int popX = (W - popW) / 2;
            int popY = (int) (150 * scaleY);
            g.setColor(Color.WHITE);
            g.fillRoundRect(popX, popY, popW, popH, 20, 30);
            int pfSize = Math.max(14, (int) (22 * Math.min(scaleX, scaleY)));
            Font pf = new Font("Fugaz one", Font.PLAIN, pfSize);
            g.setFont(pf);
            g.setColor(Color.BLACK);
            FontMetrics pfm = g.getFontMetrics(pf);
            g.drawString(popup_msg,
                    popX + (popW - pfm.stringWidth(popup_msg)) / 2,
                    popY + (popH + pfm.getAscent() - pfm.getDescent()) / 2);
        }

        if (startup_screen) {
            String msg = "Clicka per començar";
            int sfSize = Math.max(14, (int) (22 * Math.min(scaleX, scaleY)));
            Font sf = new Font("Fugaz one", Font.PLAIN, sfSize);
            g.setFont(sf);
            g.setColor(Color.WHITE);
            FontMetrics sfm = g.getFontMetrics(sf);
            g.drawString(msg,
                    (W - sfm.stringWidth(msg)) / 2,
                    (int) (530 * scaleY));
        }
    }
}
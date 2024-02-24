import java.util.HashMap;
import java.util.Map;
import java.util.Random;

public class SnakesLadders {

    private Map<Integer, Integer> ladderMap = new HashMap<>();
    private Map<Integer, Integer> snakeMap = new HashMap<>();
    private int player1Position = 0;
    private int player2Position = 0;
    private boolean isPlayer1Turn = true;

    public SnakesLadders() {
        // Ladders
        ladderMap.put(1, 38);
        ladderMap.put(4, 14);
        ladderMap.put(9, 31);
        ladderMap.put(21, 42);
        ladderMap.put(28, 84);
        ladderMap.put(36, 44);
        ladderMap.put(51, 67);
        ladderMap.put(71, 91);
        ladderMap.put(80, 100);

        // Snakes
        snakeMap.put(16, 6);
        snakeMap.put(47, 26);
        snakeMap.put(49, 11);
        snakeMap.put(56, 53);
        snakeMap.put(62, 19);
        snakeMap.put(64, 60);
        snakeMap.put(87, 24);
        snakeMap.put(93, 73);
        snakeMap.put(95, 75);
        snakeMap.put(98, 78);
    }

    public void play() {
        Random dice = new Random();
        while (true) {
            int roll = dice.nextInt(6) + 1;
            if (isPlayer1Turn) {
                player1Position += roll;
                if (player1Position > 100) {
                    player1Position -= roll;
                } else {
                    if (ladderMap.containsKey(player1Position)) {
                        player1Position = ladderMap.get(player1Position);
                    } else if (snakeMap.containsKey(player1Position)) {
                        player1Position = snakeMap.get(player1Position);
                    }
                }
                System.out.println("Player 1 is on square " + player1Position);
                if (player1Position == 100) {
                    System.out.println("Player 1 wins!");
                    break;
                }
            } else {
                player2Position += roll;
                if (player2Position > 100) {
                    player2Position -= roll;
                } else {
                    if (ladderMap.containsKey(player2Position)) {
                        player2Position = ladderMap.get(player2Position);
                    } else if (snakeMap.containsKey(player2Position)) {
                        player2Position = snakeMap.get(player2Position);
                    }
                }
                System.out.println("Player 2 is on square " + player2Position);
                if (player2Position == 100) {
                    System.out.println("Player 2 wins!");
                    break;
                }
            }
            isPlayer1Turn = !isPlayer1Turn;
        }
    }

    public static void main(String[] args) {
        SnakesLadders game = new SnakesLadders();
        game.play();
    }
}

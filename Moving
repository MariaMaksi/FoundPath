import java.util.*;

public class Moving {
    public static final int BOMB = -1;
    private final int NO_WAVE = -2;//флаг, говорящий о том что волна не дошла до клетки
    private int width;
    private int height;
    private int field[][];
    private int startX;
    private int startY;
    private int finishX;
    private int finishY;
    private Vector<Point> bomb = new Vector<>();
    private int lengthPath;
    private final int dx[] = {1, 0, -1, 0, 1, -1, -1, 1};   // смещения, соответствующие соседям ячейки
    private final int dy[] = {0, 1, 0, -1, 1, -1, 1, -1};   // справа, снизу, слева и сверху
    Vector<Point> path = new Vector<>();

    Moving(int widthNew, int heightNew){
        width = widthNew;
        height = heightNew;
        startX = 0;
        startY = 0;
        finishX = width - 1;
        finishY = height - 1;
        field  = new int[width][height];
    }


    private boolean findLiPath(){
        initField();
        if (!dataCheck()) {
            return false;
        }
        spreadWave();
        if (!recoveryPath()){
            return false;
        }
        return true;
    }
    private void initField(){
        for (int i = 0; i < width; i++) {
            for (int j = 0; j < height; j++) {
                if (field[i][j] != BOMB) {
                    field[i][j] = NO_WAVE;
                }
            }
        }
    }
    private boolean dataCheck(){
        if (field[startX][startY] == BOMB || field[finishX][finishY] == BOMB || (startX == finishX  && startY == finishY)){
            return false;
        } else {
            return true;
        }
    }
    private void spreadWave(){
        field[startX][startY] = 0;
        boolean flag = true; //наличие свободных клеток в поле
        int wave = 0;
        while ( flag == true && field[finishX][finishY] == NO_WAVE){
            flag = false;
            for (int x = 0; x < width; x++) {
                for (int y = 0; y < height; y++) {
                    if(field[x][y] == wave){
                        for (int i = 0; i < dx.length; i++) {
                            int iX = x + dx[i];
                            int iY = y + dy[i];
                            if (iX >= 0 && iX < width && iY >= 0 && iY < height && field[iX][iY] == NO_WAVE){
                                field[iX][iY] = wave + 1;
                                flag = true;
                            }
                        }
                    }
                }
            }
            wave++;
        }
    }
    private boolean recoveryPath(){
        if (field[finishX][finishY] == NO_WAVE){
            return  false; //путь невозможно найти
        }
        lengthPath = field[finishX][finishY];
        int x = finishX;
        int y = finishY;
        while (lengthPath >0){
            path.add(new Point(x,y));
            lengthPath--;
            for (int i = 0; i < dx.length; i++) {
                int iX = x + dx[i];
                int iY = y + dy[i];
                if(iX >= 0 && iX < width && iY >= 0 && iY < height && field[iX][iY] == lengthPath){
                    x = iX;
                    y = iY;
                    break;
                }

            }
        }
        if(path.size() != 1){
            path.remove(0);
        }
        return true; //путь найден
    }

    public void setStart(int startX, int startY) {
        this.startX = startX;
        this.startY = startY;
    }
    public void setFinish(int finishX, int finishY) {
        this.finishX = finishX;
        this.finishY = finishY;
    }
    public void addBomb(int x, int y){
        if( field[x][y] != BOMB){
            field[x][y] = BOMB;
        } else {
            field[x][y] = NO_WAVE;
        }
    }
    
    public Vector<Point> getPath() {
        path.clear();
        findLiPath();
        return path;
    }

    public int[][] getField() {
        return field;
    }

    public int getStartX() {
        return startX;
    }

    public int getStartY() {
        return startY;
    }

    public int getFinishX() {
        return finishX;
    }

    public int getFinishY() {
        return finishY;
    }
}

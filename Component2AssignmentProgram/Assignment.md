package project;

public class MainClass {
    public static void main(String[] args) {
        MyRailway railway = new MyRailway();
    }
}
package project;

import uk.ac.leedsbeckett.oop.Locomotive;
import uk.ac.leedsbeckett.oop.GameWorld;


 
public class NewLoco extends Locomotive {

    private static final int SLOW_SPEED = 1; // 1 pixel per tick instead of default

    public NewLoco(GameWorld world, int x, int y) {
        super(world, x, y);
        setAnimationStepPixels(SLOW_SPEED);
    }

    
    public String toString() {
        return "NewLoco [position=" + getCellPosition() + "]";
    }
}
package project;

import uk.ac.leedsbeckett.oop.OOPrailwaySim;
import uk.ac.leedsbeckett.oop.Locomotive;
import uk.ac.leedsbeckett.oop.Carriage;
 
import javax.swing.JOptionPane;
import java.util.ArrayList;
import java.util.HashSet;
import java.util.Scanner;
import java.util.Set;
 

public class MyRailway extends OOPrailwaySim {
 
    // Req 4 - Derailment tracking
    private Set<Integer> derailedLocos = new HashSet<>();
 
    
    public MyRailway() {
        super();
        about();
        startConsoleInput();
    }
 
    
    @Override
    public void about() {
        super.about();
        JOptionPane.showMessageDialog(null,
                "Extended by: Soniya Upreti\nStudent ID: 7686080",
                "About", JOptionPane.INFORMATION_MESSAGE);
    }
 
 
    @Override
    public void onTick() {
        super.onTick();
 
        ArrayList<Locomotive> locos = getLocomotives();
        if (locos == null) return;
 
        for (int i = 0; i < locos.size(); i++) {
            Locomotive loco = locos.get(i);
            int locoId = i + 1;
 
            if (loco.isDerailed()) {
                if (!derailedLocos.contains(locoId)) {
                    derailedLocos.add(locoId);
                    // Derailment is normal gameplay - just display message
                    displayMessage("Loco #" + locoId + " has derailed!", 1);
                    System.out.println("Loco #" + locoId + " has derailed!");
                }
            } else {
                derailedLocos.remove(locoId);
            }
        }
    }
 
    
    @Override
    public void processCommand(String command) {
        if (command == null || command.trim().isEmpty()) {
            return;
        }
 
        String[] parts = command.trim().split("\\s+");
        String cmd = parts[0].toLowerCase();
 
        switch (cmd) {
 
            case "about":
                about();
                break;
 
            case "start":
                startSimulation();
                break;
 
            case "stop":
                stopSimulation();
                break;
 
            case "reset":
                resetSimulation();
                derailedLocos.clear();
                break;
 
            case "addloco":
                handleAddLoco(parts);
                break;
 
            case "addslowloco":
                handleAddSlowLoco(parts);
                break;
 
            case "attachcarriage":
                handleAttachCarriage(parts);
                break;
 
            case "detachcarriage":
                handleDetachCarriage(parts);
                break;
 
            case "speed":
                handleSpeed(parts);
                break;
 
            case "crossing":
                handleCrossing(parts);
                break;
 
            default:
                showError("Unknown command: \"" + cmd + "\"\n"
                        + "Valid commands: start, stop, reset, about,\n"
                        + "addloco <x> <y>, addslowloco <x> <y>,\n"
                        + "attachcarriage <loco>, detachcarriage <loco>,\n"
                        + "speed <loco> <speed>, crossing <crossing>");
                break;
        }
    }
 
    
 
    private void handleAddLoco(String[] parts) {
        if (parts.length < 3) {
            showError("Missing parameters.\nUsage: addloco <x> <y>");
            return;
        }
        int x, y;
        try {
            x = Integer.parseInt(parts[1]);
            y = Integer.parseInt(parts[2]);
        } catch (NumberFormatException e) {
            showError("Parameters must be integers.\nUsage: addloco <x> <y>");
            return;
        }
        if (x < 0 || y < 0) {
            showError("Coordinates must not be negative.");
            return;
        }
        try {
            Locomotive loco = new Locomotive(getWorld(), x, y);
            addLocomotive(loco);
        } catch (Exception e) {
            showError("Cannot add locomotive:\n" + e.getMessage());
        }
    }
 
    private void handleAddSlowLoco(String[] parts) {
        if (parts.length < 3) {
            showError("Missing parameters.\nUsage: addslowloco <x> <y>");
            return;
        }
        int x, y;
        try {
            x = Integer.parseInt(parts[1]);
            y = Integer.parseInt(parts[2]);
        } catch (NumberFormatException e) {
            showError("Parameters must be integers.\nUsage: addslowloco <x> <y>");
            return;
        }
        if (x < 0 || y < 0) {
            showError("Coordinates must not be negative.");
            return;
        }
        try {
            NewLoco slowLoco = new NewLoco(getWorld(), x, y);
            addLocomotive(slowLoco);
        } catch (Exception e) {
            showError("Cannot add slow locomotive:\n" + e.getMessage());
        }
    }
 
    private void handleAttachCarriage(String[] parts) {
        if (parts.length < 2) {
            showError("Missing parameter.\nUsage: attachcarriage <loco>");
            return;
        }
        int locoId;
        try {
            locoId = Integer.parseInt(parts[1]);
        } catch (NumberFormatException e) {
            showError("Loco ID must be an integer.\nUsage: attachcarriage <loco>");
            return;
        }
        if (locoId < 1) {
            showError("Loco ID must be 1 or greater.");
            return;
        }
        try {
            Carriage carriage = new Carriage(getWorld());
            addCarriageToLocomotive(locoId, carriage);
        } catch (Exception e) {
            showError("Cannot attach carriage:\n" + e.getMessage());
        }
    }
 
    private void handleDetachCarriage(String[] parts) {
        if (parts.length < 2) {
            showError("Missing parameter.\nUsage: detachcarriage <loco>");
            return;
        }
        int locoId;
        try {
            locoId = Integer.parseInt(parts[1]);
        } catch (NumberFormatException e) {
            showError("Loco ID must be an integer.\nUsage: detachcarriage <loco>");
            return;
        }
        if (locoId < 1) {
            showError("Loco ID must be 1 or greater.");
            return;
        }
        try {
            detachCarriageFromLocomotive(locoId);
        } catch (Exception e) {
            showError("Cannot detach carriage:\n" + e.getMessage());
        }
    }
 
    private void handleSpeed(String[] parts) {
        if (parts.length < 3) {
            showError("Missing parameters.\nUsage: speed <loco> <speed>");
            return;
        }
        int locoId, speed;
        try {
            locoId = Integer.parseInt(parts[1]);
            speed  = Integer.parseInt(parts[2]);
        } catch (NumberFormatException e) {
            showError("Loco ID and speed must be integers.\nUsage: speed <loco> <speed>");
            return;
        }
        if (locoId < 1) {
            showError("Loco ID must be 1 or greater.");
            return;
        }
        if (speed < 0) {
            showError("Speed must not be negative.");
            return;
        }
        try {
            setLocomotiveSpeed(locoId, speed);
        } catch (Exception e) {
            showError("Cannot set speed:\n" + e.getMessage());
        }
    }
 
    private void handleCrossing(String[] parts) {
        if (parts.length < 2) {
            showError("Missing parameter.\nUsage: crossing <crossing>");
            return;
        }
        int crossingId;
        try {
            crossingId = Integer.parseInt(parts[1]);
        } catch (NumberFormatException e) {
            showError("Crossing ID must be an integer.\nUsage: crossing <crossing>");
            return;
        }
        if (crossingId < 0) {
            showError("Crossing ID must not be negative.");
            return;
        }
        try {
            toggleCrossing(crossingId);
        } catch (Exception e) {
            showError("Cannot toggle crossing:\n" + e.getMessage());
        }
    }
 
 
    private void startConsoleInput() {
        Thread consoleThread = new Thread(() -> {
            Scanner scanner = new Scanner(System.in);
            System.out.println("Railway Simulation ready. Type commands below:");
            while (true) {
                if (scanner.hasNextLine()) {
                    String line = scanner.nextLine();
                    processCommand(line);
                }
            }
        });
        consoleThread.setDaemon(true);
        consoleThread.start();
    }
 

    private void showError(String message) {
        System.err.println("ERROR: " + message);
        JOptionPane.showMessageDialog(null, message, "Error", JOptionPane.ERROR_MESSAGE);
    }
}

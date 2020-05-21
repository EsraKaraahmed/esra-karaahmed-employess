# esra-karaahmed-employess
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Scanner;

public class Homework {
    public static void main(String[] args) {
        Scanner scan = new Scanner(System.in);


        HashMap<List<String>, List<LocalDate>> map = new HashMap<>();//create map with key= id list and value = dates list

        String input = scan.nextLine();
        while (!input.equals("checkout")) { //create cycle
            List<String> id = new ArrayList<>(); // create list with the ids
            List<LocalDate> dates = new ArrayList<>();

            String[] items = input.split(", ");
            String empID = items[0];
            id.add(0, empID); //adding to the list id of index 0
            String projectID = items[1];
            id.add(1, projectID);//adding to the list id of index 1

            String dateFrom = items[2];
            DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy-MM-dd");
            LocalDate dateF = LocalDate.parse(dateFrom, formatter);  //parsing the string to LocalDate type
            dates.add(0, dateF); //adding to the dates list the dateFrom of index 0

            if (items[3].equals("NULL")) {
                LocalDate dateTo = LocalDate.now(); //reading the day like"today"
                dates.add(1, dateTo); //adding to the dates list the dateTo of index 1

            } else {
                String dateTo = items[3];
                DateTimeFormatter formatterDateTo = DateTimeFormatter.ofPattern("yyyy-MM-dd");
                LocalDate dateT = LocalDate.parse(dateTo, formatterDateTo); //parsing the string to LocalDate type
                dates.add(1, dateT);//adding to the dates list the dateTo of index 1

            }
            map.put(id, dates);//adding the list id as key of the map and the list dates as the value of the map
            input = scan.nextLine();
        }

        map.entrySet()
                .stream()
                .sorted((p1, p2) -> {
                    String projectID1 = p1.getKey().get(1);
                    String projectID2 = p2.getKey().get(1);

                    String empID1 = p1.getKey().get(0);
                    String empID2 = p2.getKey().get(0);
                    if (!projectID1.equals(projectID2)) {
                        return projectID1.compareTo(projectID2);
                    } else {
                        return empID1.compareTo(empID2);
                    }

                })
                .forEach(entry -> System.out.println(String
                        .format("%s %s %s %s",
                                entry.getKey().get(0),
                                entry.getKey().get(1),
                                entry.getValue().get(0).toString(),
                                entry.getValue().get(1).toString())));


    }
}

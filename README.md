# 03.Shopping
SoftUni_final_exam_retake
package P03;

import java.util.*;



public class P03Shopping {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        Map<String, List<String>> map = new LinkedHashMap<>();
        String inp = input.nextLine();
        String store = "";
        List<String> important = new ArrayList<>();
        while (!inp.equals("Go Shopping")) {
            store = inp.split("->")[1];
            if (inp.contains("Add")) {

                String[] listInfo = inp.split("->")[2].split(",");

                if (map.containsKey(store)) {
                    List<String> toAdd = new ArrayList<>();

                    for (int i = 0; i < listInfo.length; i++) {
                        boolean exists = false;
                        for (List<String> list : map.values()) {

                            if (list.contains(listInfo[i])) {
                                exists = true;
                            }
                        }
                        if (!exists) {
                            toAdd.add(listInfo[i]);
                        }
                    }
                    map.putIfAbsent(store, toAdd);
                } else {
                    List<String> l = new ArrayList<>();
                    for (int i = 0; i < listInfo.length; i++) {
                        boolean exists = false;
                        for (List<String> list : map.values()) {
                            if (list.contains(listInfo[i])) {
                                exists = true;
                            }
                        }
                        if (!exists) {
                            l.add(listInfo[i]);
                        }
                    }
                    map.putIfAbsent(store, l);
                }
            } else if (inp.contains("Important")) {
                String item = inp.split("->")[2];
                important.add(item);
                if (map.containsKey(store)) {
                    map.get(store).add(0, item);
                } else {
                    map.put(store, new ArrayList<>());
                    map.get(store).add(item);

                }
            } else if (inp.contains("Remove")) {
                for (int i = 0; i < important.size(); i++) {
                     if (map.containsValue(important.get(i))) {
                         if (map.containsKey(store)) {
                             map.remove(store);


                        }
                    }
                }
            }


            inp = input.nextLine();
        }
        for (Map.Entry<String, List<String>> entry : map.entrySet()) {
            System.out.printf("%s:%n", entry.getKey());
            entry.getValue().forEach(item -> System.out.println("- " + item));
        }

    }
}

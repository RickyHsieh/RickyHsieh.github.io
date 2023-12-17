---
title: Daily Leetcode - 2353. Design a Food Rating System
description: Medium priorityQueue custom comparator
date: 2023-12-17 12:00:00+0000
categories:
    - LeetCode
---

##  2023 Dec LC challenge


### 題目 2353. Design a Food Rating System

topic
* priorityQueue
* HashMap

### My Code

```java
class FoodRatings {

    public class Info {
        String food;
        String cuisine;
        int rating;

        Info(String food, String cuisine, int rating) {
            this.food = food;
            this.cuisine = cuisine;
            this.rating = rating;
        }
    }

    Map<String, Info> foodMap;
    Map<String, PriorityQueue<Info>> cuisineMap;

    public FoodRatings(String[] foods, String[] cuisines, int[] ratings) {
        foodMap = new HashMap<>();
        cuisineMap = new HashMap<>();
        for(int i = 0; i < foods.length; i++) {
           Info info = new Info(foods[i], cuisines[i], ratings[i]);
           foodMap.put(foods[i], info);

            if(cuisineMap.containsKey(cuisines[i])) {
                cuisineMap.get(cuisines[i]).add(info);
            }else{
                PriorityQueue<Info> pq = new PriorityQueue<Info>(new Comparator<Info>(){
                    @Override
                    public int compare(Info a, Info b) {
                        int result = b.rating - a.rating;
                        if (result == 0) {
                            return (a.food).compareTo(b.food);
                        }
                        return result;
                    }
                });
                pq.add(info);
                cuisineMap.put(cuisines[i],pq);
             
            }
        }
    }
    
    public void changeRating(String food, int newRating) {
        Info prev = foodMap.get(food);
        Info curr = new Info(food, prev.cuisine, newRating);
        foodMap.put(food, curr);
        prev.food = "";
        cuisineMap.get(prev.cuisine).add(curr);
    }
    
     public String highestRated(String cuisine) {
        while( cuisineMap.get(cuisine).peek().food.equals("")){
            cuisineMap.get(cuisine).remove();
        }
        return cuisineMap.get(cuisine).peek().food;
        
    }
}

/**
 * Your FoodRatings object will be instantiated and called as such:
 * FoodRatings obj = new FoodRatings(foods, cuisines, ratings);
 * obj.changeRating(food,newRating);
 * String param_2 = obj.highestRated(cuisine);
 */
```

#### foodMap結構
```java
foodMap = {
    "kimchi": Info("kimchi", "korean", 5),
    "sushi": Info("sushi", "japanese", 8),
    "ramen": Info("ramen", "japanese", 7),
    "tacos": Info("tacos", "mexican", 6)
}
```

#### cuisineMap結構
```java
cuisineMap = {
    "korean": PriorityQueue [ Info("kimchi", "korean", 5) ],
    "japanese": PriorityQueue [ Info("sushi", "japanese", 8), Info("ramen", "japanese", 7) ],
    "mexican": PriorityQueue [ Info("tacos", "mexican", 6) ]
}
```
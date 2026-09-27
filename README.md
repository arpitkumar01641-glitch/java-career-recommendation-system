# java-career-recommendation-system
java-career-recommendation-system
import java.util.*;

public class CareerRecommendationSystem {

    static Map<String, List<String>> careerSkillsMap = new HashMap<>();

    static void initCareers() {
        careerSkillsMap.put("Software Developer", Arrays.asList("java", "python", "problem solving", "oop"));
        careerSkillsMap.put("Data Scientist", Arrays.asList("python", "statistics", "machine learning", "sql"));
        careerSkillsMap.put("Cybersecurity Analyst", Arrays.asList("networking", "linux", "security", "problem solving"));
        careerSkillsMap.put("UI/UX Designer", Arrays.asList("design", "creativity", "figma", "communication"));
        careerSkillsMap.put("Cloud Engineer", Arrays.asList("aws", "linux", "networking", "docker"));
        careerSkillsMap.put("Business Analyst", Arrays.asList("excel", "communication", "sql", "problem solving"));
    }

    static List<String> recommendCareers(Set<String> userSkills) {
        Map<String, Double> matchPercent = new HashMap<>();

        for (Map.Entry<String, List<String>> entry : careerSkillsMap.entrySet()) {
            int matched = 0;
            for (String skill : entry.getValue()) {
                if (userSkills.contains(skill.toLowerCase())) matched++;
            }
            double percent = (matched * 100.0) / entry.getValue().size();
            matchPercent.put(entry.getKey(), percent);
        }

        List<Map.Entry<String, Double>> sorted = new ArrayList<>(matchPercent.entrySet());
        sorted.sort((a, b) -> Double.compare(b.getValue(), a.getValue()));

        List<String> result = new ArrayList<>();
        for (Map.Entry<String, Double> e : sorted) {
            if (e.getValue() > 0)
                result.add(String.format("%s - %.0f%% match", e.getKey(), e.getValue()));
        }
        return result;
    }

    public static void main(String[] args) {
        initCareers();

        Set<String> userSkills = new HashSet<>(Arrays.asList(
                "java", "problem solving", "sql", "communication"
        ));

        List<String> recommendations = recommendCareers(userSkills);

        System.out.println("=== Career Recommendations ===\n");
        for (String r : recommendations) {
            System.out.println("- " + r);
        }
    }
}

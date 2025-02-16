# EarTrainer
O **EarTrainer** é uma API RESTful em Java 21, usando Spring, Gradle e Railway, para treinar a percepção musical de intervalos e acordes com atividades interativas e níveis progressivos.
Ele oferece atividades interativas onde os usuários podem ouvir sons e identificar notas, intervalos ou acordes corretamente. O objetivo é aprimorar o ouvido musical de forma progressiva, com diferentes níveis de dificuldade.

Desenvolvido para o projeto final do curso de GFT Desenvolvendo em Java com IA da DIO

## Principais funcionalidades:
- **Seleção de nível**: O usuário pode escolher entre níveis iniciante, intermediário e avançado para cada atividade.
- **Treinamento auditivo:** Atividades para reconhecer acordes e intervalos musicais por meio da audição.
- **Validação de respostas:** O usuário recebe feedback se sua resposta está correta ou errada.
- Autenticação e perfil:** Login via email/senha ou Google OAuth, com um perfil personalizável.
Redes sociais: O usuário pode adicionar e editar suas redes sociais dentro do perfil.

## UX/UI (Figma)

[Acessar >>](https://www.figma.com/design/nWdoJYqm70ZisZ8qdeG17V/EarTrainer?node-id=0-1&t=5aYB5z8hnFgClNc2-1)

## UML
```classDiagram
    class EarTrainer {
        - User user
        - Activity activity
        - Level level
        - Model model  // IA (TensorFlow) para classificação e geração dinâmica
        + selectLevel(Level level)
        + selectActivity(Activity activity)
        + startSession()
        + generateIntervalOrChord(Level level)  // Geração dinâmica de intervalos e acordes
        + provideFeedback(String userAnswer)  // Feedback baseado na IA
    }

    class User {
        - String name
        - String email
        - String profileImage
        - List<SocialLink> socialLinks
        - int score  // Pontuação para medir o progresso do usuário
        + editProfile(String name, String email, String profileImage)
        + addSocialLink(SocialLink link)
        + updateScore(int points)  // Atualiza a pontuação do usuário
    }

    class SocialLink {
        - String platform
        - String url
    }

    class Activity {
        - String type // e.g., Chords, Intervals
        - List<Level> levels
        + start()
    }

    class Level {
        - String difficulty // Beginner, Intermediate, Advanced
        - List<Question> questions
        + loadQuestions()
        + adjustDifficulty(int score)  // Ajuste de dificuldade com base no progresso
    }

    class Question {
        - String soundClip
        - String correctAnswer
        - String userAnswer
        + validateAnswer(String userAnswer)
    }

    class Authentication {
        + login(String email, String password)
        + loginWithGoogle()
    }

    class Subscription {
        - boolean isSubscribed
        + subscribe()
        + unsubscribe()
    }

    class Model {
        - String modelPath // Caminho do modelo treinado (TensorFlow)
        + loadModel()  // Carrega o modelo treinado de IA
        + generateIntervalOrChord(Level level)  // Gera intervalos e acordes com IA
        + evaluateAnswer(String userAnswer, String correctAnswer)  // Avalia a resposta do usuário
    }

    EarTrainer --> User
    EarTrainer --> Activity
    EarTrainer --> Level
    EarTrainer --> Model  // Integração com IA (TensorFlow)
    User --> SocialLink
    Activity --> Level
    Level --> Question
    Level --> Model  // Ajuste de nível com base nas recomendações do modelo
    Question --> Model  // Validação da resposta com IA

```


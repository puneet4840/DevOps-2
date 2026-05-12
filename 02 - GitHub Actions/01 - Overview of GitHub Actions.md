# Overview of GitHub Actions

GitHub Actions ek automation tool hai jo GitHub ke andar built-in aata hai. Iska use karke tum automatically tasks run kara sakte ho jab bhi koi event hota hai.

Jaise:
- Code push hua
- Pull Request aayi
- Issue create hua
- Daily scheduled task
- Manual button click

Tab GitHub automatically kuch kaam kar sakta hai.

GitHub Actions automation tool hai jo workflows automate karta hai. Workflow ka matlab series of steps jo yaml file mein likhte hain aur Jab bhi repository mein koi event ho (jaise code push, PR create, release, issue create) ye yaml file mein likhe steps execute hote hain.

<br>

### Real-Life Example

Suppose tum ek Java/Spring Boot API bana rahe ho.

Normally process:
- Code likha
- GitHub par push kiya
- Server par login kiya
- Code pull kiya.
- Build kiya
- Deploy kiya
- Restart kiya

Ye sab manual hai.

**GitHub Actions kya karega?**

Jaise hi tum ```git push``` karoge:
- Automatic build
- Automatic tests
- Docker image build
- AWS/Azure par deploy
- Slack notification

Sab automatically.

Yehi hota hai: **CI/CD**.

**CI/CD**:
- CI = Continuous Integration
- CD = Continuous Deployment/Delivery

<br>
<br>

### How to create CI/CD pipeline in GitHub Actions

GitHub mein ek tab hota hota hai ```Actions``` naam se, wha click karne ek page open hota hai jisme pre-configured templates hoti hain. Ye to un templates ko use karlo jo task ke according pipeline struture define kar deti hain ya fir manually pipeline file create karlo.

**Manually Creating Pipeline**:

GitHub repository mein ye folder create karo:
```
.github/workflows/
```

Is folder ke ander tumhari yaml pipeline create hoti hai.

Structure:
```
my-java-app/
 └── .github/
      └── workflows/
           └── ci-cd.yml
```

```ci-cd.yml``` file ander tumko yaml sintax likhna hota hai.


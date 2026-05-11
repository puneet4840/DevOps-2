# Overview of GitHub Actions

GitHub Actions ek automation tool hai jo GitHub ke andar built-in aata hai. Iska use karke tum automatically tasks run kara sakte ho jab bhi koi event hota hai.

Jaise:
- Code push hua
- Pull Request aayi
- Issue create hua
- Daily scheduled task
- Manual button click

Tab GitHub automatically kuch kaam kar sakta hai.

GitHub Actions se task ko automate karwa sakte hain.

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


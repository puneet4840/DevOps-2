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

Workflow ek yaml file hai jisme series of steps likhe hote hain.

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
```
.github/workflows/ci-cd.yml
```
yahi yaml pipeline hai. Iska naam tum kuch bhi rakh sakte ho.

Structure:
```
my-java-app/
 └── .github/
      └── workflows/
           └── ci-cd.yml
```

```ci-cd.yml``` file ander tumko pipeline ka yaml syntax likhna hota hai.

<br>
<br>

### Structure of a Workflow Pipeline

GitHub Actions mein pipeline ko **Workflow** bolte hain. Ye ek YAML file hoti hai jo repository ke andar store hoti hai.

Location:
```
.github/workflows/
```

Example:
```
.github/workflows/main.yml
```

**Basic Workflow Structure**:

Ye ek minimum working GitHub Actions pipeline hai: Matlab github workflow ka basic structure esa hota hai.

```main.yaml```:
```
name: My First Pipeline

on:
  push:

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4

      - name: Print Message
        run: echo "Hello DevOps"
```

### Ab isko line by line samjhte hain:

**1. name**:
```
name: My First Pipeline
```

Ye workflow ka naam hota hai. GitHub UI mein isi naam se pipeline dikhegi.

Ye sirf identification ke liye hota hai. Agar multiple workflows hain toh easily samajh aa jata hai kaunsi pipeline chal rahi hai.

<br>
<br>

**2. on**:

```
on:
  push:
```

Ye trigger define karta hai ki workflow kab run hoga.

Yahan:
```
push
```
ka matlab hai Jab bhi koi code push hoga repository mein tab pipeline run hogi. Kisi bhi pipeline mein code push ho to pipeline run ho jayegi.

**Common Triggers**:

Matlab pipeline kab-kab run ho sakti hai.

2.1 - Push Trigger:
```
on:
  push:
```
Matlab:
- Jab bhi koi code repository yaani repo ki kisi bhi branch mein push karega workflow run hoga.

<br>

2.2 - Push on Specific Branch:
```
on:
  push:
    branches:
      - main
```

Agar kisi particular branch mein code push hone ke baad pipeline run karni hai to ye code likhna padega. Is code mein ```main``` branch mein code push hone par pipeline run hogi.

<br>

2.3 - Multiple Branches:
```
on:
  push:
    branches:
      - main
      - dev
```

Agar multiple branches mein code push hone par pipeline run karni hai to apko multiple branches likhni hain.

<br>

2.4 - Pull Request Trigger:
```
on:
  pull_request:
```
Jab repo ki kisi branch mein pull request aayegi to pipeline run hogi.


<br>

2.5 - Specifi Branch Pull Request Trigger:
```
on:
  pull_request:
    branches:
      - main
```
Jab kisi specific branch mein pull request aayegi to pipeline run hogi.

<br>

2.6 - Manual Trigger:
```
on:
  workflow_dispatch:
```
Agar aapko manual pipeline run karni hai to ```workflow_dispatch``` likhna hoga tab pipeline run karne ke liye GitHub UI mein “Run Workflow” button aa jata hai.

<br>

2.7 - Multiple Triggers:
```
on:
  push:
    branches:
      - main

  pull_request:

  workflow_dispatch:
```
Ek hi workflow multiple events pe trigger ho sakta hai.

<br>
<br>

**3. jobs**:
```
jobs:
  build:  #Job Name
    runs-on: ubuntu-latest  #Server on which job is running.
```

Workflow ke andar multiple jobs ho sakti hain.

Job = ek logical task.

Example:
- Build
- Test
- Deploy
- Security Scan

<br>

```build```:
```
build:
```
Ye job ka naam/id hai.

Aap kuch bhi naam de sakte ho:
- ```backend-build:```
- ```frontend-test:```
- ```deploy-prod:```

<br>

```runs-on```:

GitHub Actions mein jab aap koi workflow banate hain, to uski har ek job kisi na kisi runner (server) par execute hoti hai. Runner decide karne ke liye aap workflow file (.yml) mein ```runs-on``` keyword ka use karte hain.

```
runs-on: ubuntu-latest
```
Ye define karta hai Pipeline kis machine pe chalegi?

GitHub aapko do tarah ke runners deta hai:
- GitHub Runner.
- Self-Hosted runner.

GitHub Runner:
- Tumhare jobs ko run karne ke liye GitHub khud ka server provide karta hai jispe jobs run karti hain.

Common GitHub Runner:
| Runner         | Meaning       |
| -------------- | ------------- |
| ubuntu-latest  | Linux machine |
| windows-latest | Windows VM    |
| macos-latest   | Mac machine   |

Self-Hosted Runner.
- Tum khud ki machine ko github ko dete ho aur github jobs ko tumhare machines par run karta hai.

Ye Kaise Kaam Karta Hai?

Jab workflow start hoti hai:
- GitHub aapki ```runs-on: ubuntu-latest``` line ko padhta hai aur apne cloud se ek fresh Ubuntu virtual machine (VM) allocate karta h.
- Runner us VM ke andar aapke saare steps ko ek-ek karke run karta hai (jaise code checkout karna aur script chalana).
- Job khatam hone ke baad, GitHub us VM ko delete kar deta hai taaki aapka data safe rahe.

To kya alag-alag jobs ke liye humko alag-alag runners dene hote hain?

Nahi, yeh bilkul zaroori nahi hai. Aap ek hi runner par saari jobs chalate hain ya alag-alag par, yeh is baat par depend karta hai ki aapne .yml file mein kya likha hai.

<br>

Option 1: Sabhi Jobs Ke Liye Ek Hi Runner (Default):

Agar aap chahein to apni saari jobs ko ek hi tarah ke runner (jaise Ubuntu) par chalne ke liye set kar sakte hain. Lekin dhyan rahe, har job ke liye GitHub background mein ek fresh (naya) VM container kholta hai.
```
jobs:
  lint-code:
    runs-on: ubuntu-latest # Pehli job Ubuntu par chalegi
    steps:
      - run: echo "Code check ho raha hai..."

  test-code:
    runs-on: ubuntu-latest # Dusri job bhi naye Ubuntu par chalegi
    steps:
      - run: echo "Testing ho rahi hai..."
```

Option 2: Alag-Alag Jobs Ke Liye Alag-Alag Runners (Cross-Platform):

Agar aapko apna app alag-alag Operating Systems par test karna hai, to aap har job ke liye alag runner de sakte hain. Yeh sabhi jobs GitHub par ek saath (parallel mein) chalengi.
```
jobs:
  mac-build:
    runs-on: macos-latest # Apple runner par chalega
    steps:
      - run: echo "iOS/Mac app build ho raha hai..."

  windows-build:
    runs-on: windows-latest # Windows runner par chalega
    steps:
      - run: echo "Windows app build ho raha hai..."
```

Chahe aap same runner (ubuntu-latest) likhein ya alag, har job ka server bilkul alag hota hai. Jo file aapne lint-code job mein banayi hai, woh test-code job ko nahi milegi, jab tak aap use Artifacts ke zariye share na karein.


## **2.6. Branch와 Merge의 최적 활용 전략 (민정) → 이름 수정: Git branching strategies**

<aside>
🚨 효과적인 Branch 관리 전략(예: Git Flow, GitHub Flow, Branch Naming Convention, PR Convention 등), Merge 시 주의해야 할 점 및 최선의 실습 방법

- **git branch 전략 →** [https://velog.io/@kw2577/Git-branch-전략](https://velog.io/@kw2577/Git-branch-%EC%A0%84%EB%9E%B5)
    - gitflow
        - **master** : 기준이 되는 브랜치로 제품을 배포하는 브랜치
        - **develop** : 개발 브랜치로 개발자들이 이 브랜치를 기준으로 각자 작업한 기능들을 Merge
        - **feature** : 단위 기능을 개발하는 브랜치로 기능 개발이 완료되면 develop 브랜치에 Merge
        - **release** : 배포를 위해 master 브랜치로 보내기 전에 먼저 QA(품질검사)를 하기위한 브랜치
        - **hotfix** : master 브랜치로 배포를 했는데 버그가 생겼을 떄 긴급 수정하는 브랜치
    - github flow
    - gitlab flow
    - fork 와 pull request
</aside>

### What is a branching strategy

브랜치는 주로 팀이 코드를 위한 별도의 작업 공간을 제공하여 기능을 개발하는 수단으로 사용된다. 이러한 브랜치는 일반적으로 작업이 완료되면 마스터 브랜치로 다시 병합된다. 이렇게 하면 기능(및 모든 버그와 버그 수정 사항)이 서로 분리되어 유지되므로 실수를 더 쉽게 수정할 수 있다.

Branches are primarily used as a means for teams to develop features giving them a separate workspace for their code. These branches are usually merged back to a master branch upon completion of work. In this way, features (and any bug and bug fixes) are kept apart from each other allowing you to fix mistakes more easily.

즉, 브랜치는 코드의 메인라인을 보호하고 특정 브랜치에 대한 변경 사항이 다른 개발자에게 영향을 미치지 않는다.

This means that branches protect the mainline of code and any changes made to any given branch don’t affect other developers.

**따라서 브랜치 전략은 소프트웨어 개발팀이 버전 관리 시스템을 사용할 때 코드를 작성, 병합 및 배포할 때 채택하는 전략이다.**

**A branching strategy, therefore, is the strategy that software development teams adopt when writing, merging and deploying code when using a version control system.**

이는 본질적으로 개발자가 공유 코드베이스와 상호 작용하는 방식을 규정하기 위해 따를 수 있는 일련의 규칙이다.

### Why you need a branching strategy?

It is essentially a set of rules that developers can follow to stipulate how they interact with a shared codebase.

이러한 전략은 여러 개발자가 동시에 작업하면서 동시에 변경 사항을 추가할 때 애플리케이션의 오류와 끔찍한 병합 지옥을 피하기 위해 리포지토리를 체계적으로 유지하는 데 도움이 되므로 필요하다.

Such a strategy is necessary as it helps keep repositories organized to avoid errors in the application and the dreaded merge hell when multiple developers are working simultaneously and are all adding their changes at the same time.

(아래는 요약한 내용)

- neccesary to
    - avoid conflicts when merging / 병합 시 충돌을 방지하고
    - allow for the easier integration of changes into the master trunk / 변경 사항을 마스터 트렁크에 쉽게 통합할 수 있도록 하기 위해 필요

**브랜치 전략의 목표:** 

**A branching strategy aims to:**

- Enhance productivity by ensuring proper coordination among developers
- Enable parallel development
- Help organize a series of planned, structured releases
- Map a clear path when making changes to software through to production
- Maintain a bug-free code where developers can quickly fix issues and get these changes back to production without disrupting the development workflow

- 개발자 간의 적절한 조정을 통해 생산성 향상
- 병렬 개발 활성화
- 일련의 계획적이고 체계적인 릴리스를 구성하는 데 도움을 줌
- 소프트웨어를 변경할 때 프로덕션까지 명확한 경로를 매핑함
- 개발자가 문제를 신속하게 수정하고 개발 워크플로우를 중단하지 않고 변경 사항을 프로덕션에 적용할 수 있는 버그 없는 코드 유지

### Common Git branching strategies

> **GitFlow**
> 

Gitflow는 오늘날 많은 프로젝트에서 다소 복잡하고 고급으로 간주되고 있다. Gitflow를 사용하면 개발자가 마스터 브랜치에서 기능 브랜치를 생성하는 기능에 대해 마스터 브랜치와 별도로 작업할 수 있는 병렬 개발이 가능하다.

Considered to be a bit complicated and advanced for many of today’s projects, GitFlow enables parallel development where developers can work separately from the master branch on features where a feature branch is created from the master branch.

나중에 변경이 완료되면 개발자는 이러한 변경 사항을 마스터 브랜치에 다시 병합하여 릴리스한다.

Afterwards, when changes are complete, the developer merges these changes back to the master branch for release.

이 브랜치 전략은 다음과 같은 브랜치로 구성된다.

**This branching strategy consists of the following branches:**

- **Master**
- **Develop**
- **Feature**: - to develop new features that branches off the develop branch
    - 개발 브랜치에서 브랜치되는 새로운 기능을 개발하는 데 사용됨
- **Release**: - help prepare a new production release; usually branched from the develop branch and must be merged back to both develop and master
    - 새 프로덕션 릴리스를 준비하는 데 도움이 되며, 일반적으로 개발 브랜치에서 브랜치되며 다시 개발 브랜치와 마스터 브랜치로 병합해야 함
- **Hotfix**: also helps prepare for a release but unlike release branches, hotfix branches arise from a bug that has been discovered and must be resolved; it enables developers to keep working on their own changes on the develop branch while the bug is being fixed.
    - 역시 릴리즈 준비에 도움이 되지만 릴리즈 브랜치와 달리 핫픽스 브랜치는 발견되어 해결해야 하는 버그에서 발생하며, 개발자는 버그가 수정되는 동안 개발 브랜치에서 자체 변경 작업을 계속할 수 있다.

![출처: https://www.abtasty.com/blog/git-branching-strategies/](https://prod-files-secure.s3.us-west-2.amazonaws.com/13dd0972-4b14-4a5a-a69d-46aafd0b55bf/5b67250f-381d-4314-ba57-7e7b29341543/Untitled.png)

출처: https://www.abtasty.com/blog/git-branching-strategies/

The main and develop branches are considered to be the main branches, with an infinite lifetime, while the rest are supporting branches that are meant to aid parallel development among developers, usually short-lived.

메인 브랜치와 개발 브랜치는 수명이 무한한 메인 브랜치로 간주되며, 나머지 브랜치는 개발자들 간의 병렬 개발을 돕기 위한 지원 브랜치로 보통 수명이 짧습니다.

- **GitFlow pros and cons**
    - **Pros**
        - It allows for parallel development to protect the production code so the main branch remains stable for release while developers work on separate branches.
            
            병렬 개발을 통해 프로덕션 코드를 보호할 수 있으므로 개발자가 별도의 브랜치에서 작업하는 동안 메인 브랜치는 안정적으로 릴리스할 수 있다.
            
        - The various types of branches make it easier for developers to organize their work
            
            다양한 유형의 브랜치를 사용하면 개발자가 작업을 더 쉽게 정리할 수 있다
            
        - It is also ideal when handling multiple versions of the production code.
            
            여러 버전의 프로덕션 코드를 처리할 때 이상적입니다.
            
    - Cons
        - Developers will first need to create the release branch then make sure any final work is also merged back into the development branch and then that release branch will need to be merged into the main branch.
            
            브랜치가 추가되면 개발자가 개발 브랜치에서 메인 브랜치로 변경 사항을 병합할 때 관리가 어려워질 수 있다. 개발자는 먼저 릴리스 브랜치를 만든 다음 최종 작업이 개발 브랜치에 다시 병합되었는지 확인한 다음 해당 릴리스 브랜치를 메인 브랜치에 병합해야 한다.
            
        - In the event that changes are tested and the test fails, it would become increasingly difficult to figure out where the issue is exactly as developers are lost in a sea of commits.
            
            변경 사항을 테스트하다가 테스트가 실패하는 경우, 개발자가 수많은 커밋 속에서 길을 잃게 되므로 문제가 정확히 어디에 있는지 파악하기가 점점 더 어려워질 수 있다.
            
        - Due to GitFlow’s complexity, it could slow down the development process and release cycle. ⇒ GitFlow is not an efficient approach for teams wanting to implement continuous integration and continuous delivery.
            
            실제로 GitFlow의 복잡성으로 인해 개발 프로세스와 릴리스 주기가 느려질 수 있다. 그런 의미에서 지속적 통합과 지속적 배포를 구현하고자 하는 팀에게는 GitFlow가 효율적인 접근 방식이 아님
            
        

Thus, in that case a much simpler workflow such as GitHub Flow is recommended.

따라서 이러한 경우에는 GitHub Flow와 같은 훨씬 더 간단한 워크플로우를 사용하는 것이 좋습니다.

> **GitHubFlow**
> 

GitHub Flow is a simpler alternative to GitFlow ideal for smaller teams as they don’t need to manage multiple versions.

GitHub Flow는 여러 버전을 관리할 필요가 없으므로 소규모 팀에 적합한 GitFlow의 간단한 대안이다.

Unlike GitFlow, this model doesn’t have release branches. You start off with the main branch then developers create branches, feature branches that stem directly from the master, to isolate their work which are then merged back into main. The feature branch is then deleted.

GitFlow와 달리 이 모델에는 릴리스 브랜치가 없다. 메인 브랜치에서 시작한 다음 개발자가 마스터 브랜치에서 직접 파생된 기능 브랜치인 브랜치를 만들어 작업을 분리한 다음 다시 메인 브랜치에 병합한다. 그런 다음 기능 브랜치는 삭제된다.

The main idea behind this model is keeping the master code in a constant deployable state and hence can support continuous integration and continuous delivery processes.

이 모델의 기본 아이디어는 마스터 코드를 지속적으로 배포 가능한 상태로 유지하여 지속적인 통합 및 지속적인 배포 프로세스를 지원할 수 있다는 것이다.

> **위 내용 정리**
> 
> - What
>     - GitHub Flow is a simpler alternative to GitFlow ideal for smaller teams as they don’t need to manage multiple versions.
> - 특징
>     - Unlike GitFlow, this model doesn’t have release branches.
>     - Main branch → feature branch → merged back into main → delete feature branch
> - main idea
>     - keeping the master code in a constant deployable state
>     - can support continuous integration and continuous delivery processes.

![https://www.abtasty.com/blog/git-branching-strategies/](https://prod-files-secure.s3.us-west-2.amazonaws.com/13dd0972-4b14-4a5a-a69d-46aafd0b55bf/60f67e1e-b961-4dc9-863a-f9cef073073e/Untitled.png)

https://www.abtasty.com/blog/git-branching-strategies/

- GitHub Flow pros and cons
    - Pros
        - focuses on Agile principles and so it is a fast and streamlined branching strategy with short production cycles and frequent releases.
            
            Github Flow는 애자일 원칙에 중점을 두므로 짧은 프로덕션 주기와 빈번한 릴리스로 빠르고 능률적인 브랜칭 전략입니다.
            
        - allows for fast feedback loops so that teams can quickly identify issues and resolve them.
            
            또한 이 전략은 피드백 루프가 빠르기 때문에 팀이 문제를 빠르게 파악하고 해결할 수 있습니다.
            
        - Since there is no development branch as you are testing and automating changes to one branch which allows for quick and continuous deployment.
            
            하나의 브랜치에서 변경 사항을 테스트하고 자동화하기 때문에 개발 브랜치가 없으므로 빠르고 지속적인 배포가 가능합니다.
            
        - This strategy is particularly suited for small teams and web applications and it is ideal when you need to maintain a single production version.
            
            이 전략은 특히 소규모 팀과 웹 애플리케이션에 적합하며 단일 프로덕션 버전을 유지 관리해야 할 때 이상적입니다.
            
    - Cons
        - this strategy is not suitable for handling multiple versions of the code. 여러 버전의 코드를 처리하는 데는 적합하지 않다.
        - the lack of development branches makes this strategy more susceptible to bugs and so can lead to an unstable production code if branches are not properly tested before merging with the master-release preparation and bug fixes happen in this branch. ⇒ The master branch, as a result, can become cluttered more easily as it serves as both a production and development branch.
            
            또한 이 전략은 개발 브랜치가 없기 때문에 버그에 더 취약하므로 마스터 릴리스 준비와 병합하기 전에 브랜치를 제대로 테스트하지 않고 이 브랜치에서 버그 수정이 이루어지면 프로덕션 코드가 불안정해질 수 있다. ⇒ 결과적으로 마스터 브랜치는 프로덕션 브랜치와 개발 브랜치의 역할을 동시에 수행하기 때문에 더 쉽게 복잡해질 수 있다.
            
        - this model is more suited to small teams and hence, as teams grow merge conflicts can occur as everyone is merging to the same branch and there is a lack of transparency meaning developers cannot see what other developers are working on.
            
            소규모 팀에 더 적합하기 때문에 팀이 성장함에 따라 모든 사람이 같은 브랜치로 병합할 때 충돌이 발생할 수 있고 투명성이 부족하여 개발자가 다른 개발자가 작업 중인 내용을 볼 수 없다.
            

> **GitLab Flow**
> 

GitLab Flow is a simpler alternative to GitFlow that combines feature-driven development and feature branching with issue tracking.

GitLab Flow는 기능 중심 개발 및 기능 브랜칭과 이슈 추적을 결합한 GitFlow의 더 간단한 대안이다.

With GitFlow, developers create a develop branch and make that the default while GitLab Flow works with the main branch right away.

GitFlow를 사용하면 개발자가 개발 브랜치를 만들고 이를 기본 브랜치로 설정하는 반면, GitLab Flow는 메인 브랜치와 함께 바로 작동한다.

GitLab Flow is great when you want to maintain multiple environments and when you prefer to have a staging environment separate from the production environment. Then, whenever the main branch is ready to be deployed, you can merge back into the production branch and release it.

여러 환경을 유지 관리하고 싶을 때나 스테이징 환경을 프로덕션 환경과 분리하고 싶을 때 GitLab Flow가 유용하다. 그런 다음 메인 브랜치를 배포할 준비가 되면 언제든지 프로덕션 브랜치에 다시 병합하여 릴리스할 수 있다.

Thus, this strategy offers propers isolation between environments allowing developers to maintain several versions of software in different environments.

따라서 이 전략은 개발자가 여러 환경에서 여러 버전의 소프트웨어를 유지 관리할 수 있도록 환경 간에 적절한 격리를 제공한다.

While GitHub Flow assumes that you can deploy into production whenever you merge a feature branch into the master, GitLab Flow seeks to resolve that issue by allowing the code to pass through internal environments before it reaches production, as seen in the image below.

GitHub Flow는 기능 브랜치를 마스터에 병합할 때마다 프로덕션에 배포할 수 있다고 가정하지만, GitLab Flow는 아래 이미지에서 보는 것처럼 코드가 프로덕션에 도달하기 전에 내부 환경을 통과하도록 허용하여 이 문제를 해결하려고 한다.

> **위 내용 정리**
> 
> - What
>     - GitLab Flow is a simpler alternative to GitFlow that combines feature-driven development and feature branching with issue tracking.
> - 특징
>     - Unlike Github Flow, GitLab Flow works with the main branch right away.
>     - when you want to maintain multiple environments and when you prefer to have a staging environment separate from the production environment.
>     
> - main idea
>     - whenever the main branch is ready to be deployed, you can merge back into the production branch and release it.
>     - GitLab Flow seeks to resolve that issue by allowing the code to pass through internal environments before it reaches production, as seen in the image below.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/13dd0972-4b14-4a5a-a69d-46aafd0b55bf/362da7d3-3d82-4ac5-b388-cd2507e09d8d/Untitled.png)

Therefore, this method is suited for situations where you don’t control the timing of the release, such as an iOS app that needs to go through the App store validation first or when you have specific deployment windows.

따라서 이 방법은 앱 스토어 유효성 검사를 먼저 거쳐야 하는 iOS 앱이나 특정 배포 기간이 있는 경우와 같이 릴리스 시기를 제어할 수 없는 상황에 적합하다.

> **Trunk-based development**
> 

Trunk-based development is a branching strategy that in fact requires no branches but instead, developers integrate their changes into a shared trunk at least once a day. This shared trunk should be ready for release anytime.

트렁크 기반 개발은 실제로 브랜치가 필요 없는 대신 개발자가 하루에 한 번 이상 변경 사항을 공유 트렁크에 통합하는 브랜칭 전략이다. 이 공유 트렁크는 언제든 릴리스할 준비가 되어 있어야 한다.

The main idea behind this strategy is that developers make smaller changes more frequently and thus the goal is to limit long-lasting branches and avoid merge conflicts as all developers work on the same branch. In other words, developers commit directly into the trunk without the use of branches.

이 전략의 기본 개념은 개발자가 작은 변경을 더 자주 수행하므로 오래 지속되는 브랜치를 제한하고 모든 개발자가 동일한 브랜치에서 작업할 때 병합 충돌을 방지하는 것이다. 즉, 개발자는 브랜치를 사용하지 않고 트렁크에 직접 커밋한다.

Consequently, trunk-based development is a key enabler of continuous integration (CI) and continuous delivery (CD)  since changes are done more frequently to the trunk, often multiple times a day (CI) which allows features to be released much faster (CD).

결과적으로 트렁크 기반 개발은 지속적인 통합(CI) 및 지속적인 배포(CD)의 핵심 요소로, 트렁크에 대한 변경이 더 자주, 종종 하루에 여러 번 수행되므로(CI) 기능을 훨씬 빠르게 릴리스할 수 있다(CD).

This strategy is often combined with feature flags. As the trunk is always kept ready for release, feature flags help decouple deployment from release so any changes that are not ready can be wrapped in a feature flag and kept hidden while features that are complete can be released to end-users without delay. 

이 전략은 종종 기능 플래그와 결합되기도 한다. 트렁크는 항상 릴리스 준비가 되어 있으므로 기능 플래그는 배포와 릴리스를 분리하여 준비가 되지 않은 변경 사항은 기능 플래그에 래핑하여 숨기고, 완료된 기능은 지체 없이 최종 사용자에게 릴리스할 수 있도록 도와준다.

> **위 내용 정리**
> 
> - What
>     - Trunk-based development is a branching strategy that in fact requires no branches but instead, developers integrate their changes into a shared trunk at least once a day.
> - 특징
>     - developers make smaller changes more frequently and thus the goal is to limit long-lasting branches and avoid merge conflicts as all developers work on the same branch. ⇒ developers commit directly into the trunk without the use of branches
> - main idea
>     - trunk-based development is a key enabler of continuous integration (CI) and continuous delivery (CD)  since changes are done more frequently to the trunk, often multiple times a day (CI) which allows features to be released much faster (CD).
>     

![https://www.abtasty.com/blog/git-branching-strategies/](https://prod-files-secure.s3.us-west-2.amazonaws.com/13dd0972-4b14-4a5a-a69d-46aafd0b55bf/f95b3f56-63bb-484b-99dd-07a17247b0f2/Untitled.png)

https://www.abtasty.com/blog/git-branching-strategies/

- Pros and Cons
    - Pros
        - trunk-based development paves the way for continuous integration as the trunk is kept constantly updated.
            
             트렁크 기반 개발은 트렁크가 지속적으로 업데이트되므로 지속적인 통합을 위한 기반을 마련합니다.
            
        - It also enhances collaboration as developers have better visibility over what changes other developers are making as commits are made directly into the trunk without the need for branches.
            
            브랜치 없이 트렁크에 직접 커밋을 하기 때문에 개발자가 다른 개발자의 변경 사항을 더 잘 파악할 수 있어 협업이 향상된다 ~~(각 개발자가 자신의 브랜치에서 독립적으로 작업하고 해당 브랜치에서 발생하는 모든 변경 사항을 메인 브랜치로 병합한 후에야 확인할 수 있는 다른 브랜칭 방법과 다르다)~~
            
        - Because trunk-based development does not require branches, this eliminates the stress of long-lived branches and hence, merge conflicts or the so-called ‘merge hell’ as developers are pushing small changes much more often. This also makes it easier to resolve any conflicts that may arise.
            
            브랜치가 필요하지 않기 때문에 개발자가 작은 변경 사항을 훨씬 더 자주 푸시하기 때문에 오래 지속되는 브랜치의 스트레스를 없애고 병합 충돌이나 소위 '병합 지옥'을 방지할 수 있다 ⇒ 즉, 발생할 수 있는 충돌을 더 쉽게 해결할 수 있다.
            
        - This strategy allows for quicker releases as the shared trunk is kept in a constant releasable state with a continuous stream of work being integrated into the trunk which results in a more stable release.
            
            공유 트렁크가 지속적으로 릴리스 가능한 상태로 유지되고 지속적인 작업 스트림이 트렁크에 통합되어 보다 안정적인 릴리스가 가능하므로 더 빠른 릴리스가 가능하다.
            
    - Cons
        - This strategy is suited to more senior developers as this strategy offers a great amount of autonomy which non-experienced developers might find daunting as they are interacting directly with the shared trunk.
            
            공유 트렁크와 직접 상호 작용하기 때문에 경험이 없는 개발자가 부담스러워할 수 있는 상당한 자율성을 제공하므로 시니어급 개발자에게 적합하다
            
        

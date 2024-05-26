
### **How to choose the best branching strategy for your team**

- Github Flow of Trunk-based development:
    
    When first starting out, it’s best to keep things simple and so initially GitHub Flow or Trunk-based development may work best. They are also ideal for smaller teams requiring only a single version of a release to be maintained.
    
    처음 시작할 때는 일을 단순하게 유지하는 것이 가장 좋으므로 초기에는 GitHub Flow 또는 트렁크 기반 개발이 가장 적합할 수 있다. 또한 단일 버전의 릴리스만 유지 관리해야 하는 소규모 팀에도 이상적이다.
    
- GitFlow:
    
    GitFlow is great for open-source projects that require strict access control to changes. This is especially important as open-source projects allow anyone to contribute and so with Git Flow, you can check what is being introduced into the source code.
    
    GitFlow는 변경 사항에 대한 엄격한 액세스 제어가 필요한 오픈 소스 프로젝트에 적합하다. 오픈 소스 프로젝트에서는 누구나 기여할 수 있으므로 Git Flow를 사용하면 소스 코드에 무엇이 도입되는지 확인할 수 있으므로 특히 중요하다.
    

However, GitFlow, as previously mentioned, is not suitable when wanting to implement a DevOps environment. In this case, the other strategies discussed are a better fit for an Agile DevOps process and to support your CI and CD pipeline.

하지만 앞서 언급했듯이 GitFlow는 데브옵스 환경을 구현하고자 할 때는 적합하지 않다. 이 경우에는 앞서 설명한 다른 전략이 애자일 데브옵스 프로세스에 더 적합하고 CI 및 CD 파이프라인을 지원하는 데 더 적합하다.

| Product type and its release method | Team size | Collaboration maturity | Applicable mainstream branch mode |
| --- | --- | --- | --- |
| All | Small team | High | Trunk-Based Development (TBD) |
| Products that support continuous deployment and release, such as SaaS products | Middle | Moderate | GitHub-Flow and TBD |
| Products with a definite release window and a periodic version release cadence, such as iOS apps | Middle | Moderate | Git-Flow and GitLab-Flow with release branch |
| Products that are demanding for prodgiuct quality and support continuous deployment and release, such as basic platform products | Middle | Moderate | GitLab-Flow |
| Products that are demanding for product quality and have a long maintenance cycle for released versions, such as 2B basic platform products | Large | Moderate | Git-Flow |

To sum up, there is no such thing as the perfect strategy. The strategy you choose will depend on your team and the nature and complexity of your project and so this should be evaluated on a case-by-case basis.

요약하자면, 완벽한 전략이란 존재하지 않다. 선택하는 전략은 팀과 프로젝트의 성격 및 복잡성에 따라 달라질 수 있으므로 사례별로 평가해야 한다.

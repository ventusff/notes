---

**`"Learning Reward Functions for Optimal Highway Merging"`**
**[** `Year` **]** **[[:memo:](https://arxiv.org/) (paper)]** **[[:octocat:](https://github.com/) (code)]** **[[🎞️](https://www.youtube.com/) (video)]** **[** :mortar_board: `University X` **]** **[** :office: `company Y` **]**
**[**  John Doe  **]**
**[** _`related`, `concepts`_  **]**

<details>
  <summary>Click to expand</summary>

| ![image-20201026105747343](media/template.png) |
| :----------------------------------------------------------: |
|                                                              |

- _What?_
  
  - A Project from the Stanford course ([AA228/CS238 - Decision Making under Uncertainty](https://web.stanford.edu/class/aa228/cgi-bin/wp/)). Examples of student projects can be found [here](https://web.stanford.edu/class/aa228/cgi-bin/wp/old-projects/).
- My main takeaway:
  
  - A **simple problem** that illustrates the need for (_learning more about_) **`IRL`**.
- The **merging task** is formulated as a **simple `MDP`**:
  - The **state space** has **size `3`** and is **discretized**: `lat` + `long` ego position and `long` position of the other car.
  - The other vehicle **transitions stochastically** (`T`) according to three simple behavioural models: `fast`, `slow`, `average speed` driving.
  - The main contribution concerns the **reward design**: _how to_ **_shape the reward function_** _for this_ **_multi-objective_** _(_**_trade-off_** `safety` _/_ `efficiency`_)_ _optimization problem?_
- Two **reward functions** (`R`) are compared:
  - > `1-` "The first formulation models rewards based on **our prior knowledge** of how we **would expect** autonomous vehicles to operate, **directly encoding human values** such as `safety` and `mobility` into this problem as a positive reward for merging, a penalty for `merging close` to the other vehicle, and a penalty for `staying` in the on-ramp."
  - > `2-` "The second reward function formulation **assumes no prior knowledge** of **human values** and instead comprises a **simple degree-one polynomial** expression for the components of the `state` and the `action`."
    
    - The **parameters** are tuned using a sort of **grid search** (no proper `IRL`).
- _How to compare them?_
  - Since **both `T` and `R` are known**, a **planning** (as [opposed](https://github.com/chauvinSimon/IV19#difference-learning-vs-planning) to **learning**) algorithm can be used to find the **optimal policy**. Here `value iteration` is implemented.
  - The resulting agents are then evaluated based on **two conflicting objectives**:
    
    - > "Minimizing the distance along the road at which **point merging occurs** and **maximizing the `gap`** between the two vehicles when merging."
  - Next step will be proper **`IRL`**:
    
    - > "We can therefore conclude that there may exist **better reward functions** for capturing optimal driving policies than either the **intuitive prior knowledge** reward function or the **polynomial reward function**, which **doesn’t incorporate any human understanding of costs** associated with `safety` and `efficiency`."

</details>

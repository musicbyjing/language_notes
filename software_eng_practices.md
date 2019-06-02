# Software Engineering Practices

## Methodologies

### Waterfall

- **Linear-sequential** life cycle model
- **Predictive** rather than adaptive--depends entirely on requirement analysis
- Each phase completed before the next; no overlapping
1. Requirement analysis
   - Document requirements in a requirement specification document 
2. System design
   - Define hardware/software system architecture based on requirements
3. Implementation
   - Develop units, do unit testing 
4. Testing
   - Integration, then integration testing
5. Deployment 
7. Maintenance

#### Advantages

- Easy to use/understand
- Good for smaller projects with clear requirements

#### Disadvantages

- Doesn't allow for backtracking or revision
- Working software produced late in cycle
- High risk
- Integration done as a "big bang"

### Iterative / incremental

- Start with simple implementation of small set of software requirements, then, *iteratively* enhance features
- Start with a set of **simple requirements** (NOT full specifications), then do a build. Then, do another build.
  - Repeated cycles, small portions at a time

#### Advantages

- Working model early on, easy to find functional / design flaws

#### Disadvantages

- Best for large projects, since it's hard to break down small software into serviceable increments

### Agile

- Iterative model with cross-functional teams working simultaneously across the development process
- **Adaptive** rather than predictive (like Waterfall)
- Focus on customer interaction
- Principles:
  - Self-organization, motivation, teamwork
  - Working software > documentation
  - Customer collaboration
  - Adapt to change

#### Disadvantages

- Not suitable for complex dependencies
- Very high dependency on the individual, as there is little documentation produced

#### Scrum

- Work in **sprints** of two weeks to two months
  - Begin with planning meeting, end with review
  - Daily checkin meetings
  - Create finished portion of a product
  - *Go thru the entire software dev cycle in one sprint*
  
#### Kanban

- Work items, represented by cards, are organized on a **kanban board** where they flow from one **workflow stage** (column) to the next
  - Stages can be To Do, In Progress, Review, etc.
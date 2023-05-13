# A-TEAMs
*Autonomous LLM Agent Teams*

## Goal

Create a system that optimizes the use of LLM(s) to create high-quality complex outputs that may involve multiple work streams with multiple, multi-disciplinary work.

## Success Criteria

To be successful the system should be able to:

- Translate high-level human provided objective(s) into necessary work outputs to realize objective(s).
- Create work outputs equivalent in quality to human output for similar work.
- Provide effective collaboration and communication between human and LLMs to achieve correct work.
- Optimally utilize LLM's innate abilities.

## System Design 

### Elements

1. **Human Director**: Provides overall objective and guidance for the project.
2. **LLM Project Manager**: Focuses on high-level project organization, task decomposition, and overall progress monitoring. Works closely with the Human Director to identify required outputs, success criteria, and decompose the project into work streams. Is capable of generating multiple potential solutions or approaches to reach objectives, enabling Human Director to explore and evaluate options to select the best one based on project requirements and constraints. Determines the specialized work needed within each work stream and creates/assigns appropriate LLM Specialist(s). PM will also be responsible for overseeing the progress of work streams and adapting the work as needed, including automatically scaling the number of LLM Specialists or LLM Collaborators as needed to maintain an efficient balance between the available resources and the project's needs.
3. **LLM Specialists**: LLMs with specific priming and context management to handle specialized tasks within each work stream. They can perform tasks like research, writing, data analysis, or other domain-specific work. In some cases, a single LLM might be able to handle multiple roles by switching contexts, thus reducing the number of LLMs required.
4. **Human Specialists**: Optional; human domain experts assigned to work alongside LLM Specialists to provide insights and expertise that an LLM might not possess to help ensure high-quality outcomes. Human experts can "train" or "tutor" LLMs in specific areas, allowing LLMs to absorb and apply knowledge more effectively in their work.
5. **LLM Collaborator**: Focuses on facilitating communication and collaboration between team members, whether they are LLMs or humans. Primed to facilitate communication, coordinate tasks, and ensure smooth collaboration between team members (including verifying and distributing work in one-to-many, many-to-one, and many-to-many workflows). While the Project Manager is responsible for adjusting the project approach as needed, the Collaborator can help in identifying and addressing any communication or collaboration issues that may arise, further improving the adaptability of the system. In smaller or less complex projects, it might be possible to merge the roles of Project Manager and Collaborator into a single LLM.
6. **LLM Learning & Performance Manager**: An LLM responsible for collecting feedback and learnings from human experts and other LLMs, evaluating the performance of LLM Specialists, and updating the system messages and external memory. This LLM ensures continuous improvement and adaptation of skills and expertise by identifying best practices, providing feedback for improvement, and leveraging expertise in evaluation techniques, data analysis, and performance metrics.
7. **Tools**: utilities, software applications, APIs that assist LLMs and human team members in performing their tasks and achieving project objectives. Tools can be general-purpose or project-specific, and they facilitate various aspects of project work, including communication, data analysis, research, and content generation.
8. **Resources**: Informational assets, knowledge repositories, or ex2. pert systems that LLMs and human team members can access and utilize to enhance their understanding, inform their decision-making, and improve the quality of their work. Resources can be general-purpose or project-specific and can be provided in various formats, such as databases, documents, websites, or multimedia content.

### Structure

- Agency
	- 1 Human Director
	- 1 LLM Project Manager
	- 1 LLM Learning & Performance Manager
	- 0+ Tools (cross-project; eg. web search, APIs)
	- 0+ Resources (cross-project; eg. general knowledge repo)
	- 1+ Project(s)
		- 0+ Project-specific tools
		- 0+ Project-specific resources
		- 1+ Work stream(s)
			- 1 LLM Collaborator
			- 1+ LLM Specialist(s)
			- 0+ Human Specialist(s)

### Project Workflow

1. Within dedicated communication channel Human Director creates or invokes LLM Project Manager (PM).
2. Human Director provides PM with new project objective(s).
3. PM generates multiple potential solutions or approaches to achieve project objective(s) and works with Human Director to identify objectives' required output(s), success criteria, and work plan (decomposition of objectives' required outputs into work streams, success criteria / specialized work needed to complete work in each stream, desired level of human interaction and oversight.)
6. PM creates dedicated communication channel(s) for project work stream(s).
7. Within each work stream, PM instantiates 1 LLM Collaborator and 1+ LLM Specialists (priming LLMs with specific expertise, roles) to perform work needed to achieve work stream outputs. PM determines whether an existing Specialist can be used of if a new one needs to be created. PM determines whether to use a single LLM or multiple LLMs for Specialists based on task complexity, parallelism, context window limitations, and human interaction needs. Humans, PM, Collaborators, and Specialists within Agency all have unique ids within communication system, allowing them to be notified in specific messages. LLMs (PM, Collaborators, Specialists) have /command keywords that trigger their intended functionality - these are used within communications to trigger actions and requests between LLM : LLM  and human : LLM.
8. Within work stream channel(s) PM provides specific project tasks and context to Collaborators and Specialists.
9. Within work stream channel, Specialists document their thinking, actions, and feedback.
10. Within work stream, Collaborator enables effective collaboration and handoff of work between Specialists, and optional Human Collaborators, to exchange information, provide feedback, and iterate on their work.
11. When appropriate, Human Specialists, if present, provide training or tutoring to LLMs, helping them develop a deeper understanding of specific subject areas or methodologies, which can then be applied to improve the quality of their work.
12. PM tracks and manages dependencies between tasks and work streams, ensuring smooth progress and avoiding potential bottlenecks or conflicts. PM adjusts the allocation of resources and tasks as needed to maintain optimal project flow.
13. When work output(s) within a work stream meet success criteria PM is notified, and optionally Human Director depending upon initially determined work plan. When all work stream outputs are successfully completed PM assembles work outputs as appropriate and notifies Human Director.
14. At any point Human Director can view LLM's work (whether work in progress or complete) and provide input within communication channels to inform work iteration and refinement.
15. When work issues occur within a work stream (blockages, uncertainties ,etc) PM is alerted and attempts to resolve issues through feedback to Collaborator/Specialist or by add new Specialists, if necessary. If PM is unable to resolve/answer work issue Human Director is notified.
16. PM, Collaborator, and Specialists are able to leverage external memory to store context and memory, overcoming context window limitations and saving learned experiences for future use by similar roles.
17. LLM Learning & Performance Manager gathers feedback and learnings from human experts and other LLMs, updating the LLM Specialists' system messages and external memory accordingly, allowing LLMs to refine their expertise and improve their performance over time.
18. PM gathers insights from monitoring of work (LLM interactions, accuracy, efficacy, work blockages, response times, etc) for adjustments to refine and improve the system.
19. LLM Learning & Performance Manager assesses the performance of Specialists, comparing their outputs against established metrics and benchmarks. Provides feedback to Specialists and PM to help refine their work and improve system efficacy.

## Likely Implementation

### Infrastructure

- **LLM**
	- OpenAI API
	- GPT-3.5 as possible
	- GPT-4 when necessary
- **LLM : Human and LLM : LLM communication**
	- should afford asynchronous communication, direct messages & threaded conversations, notifications
	- should afford structuring messages by project / work stream / work
	- implement via private *Discord*
	- discord = agency
	- category = project
	- channel = project work stream
	- thread = each specialist's record of work
- **LLM Memory**
	- memory should afford saving / retrieval of:
		- Specialists role & expertise definitions
		- Specialists' observations and learnings on work feedback
		- system performance metics { *or is this better saved and referenced thru System Monitoring tool?* }
		- PM's observations and learnings from past system performance
		- task status and progress { *or is this already handled via Discord record of messages?* }
		- observed collaboration patterns and best practices from successful projects to help LLMs work more effectively together in future projects
		- lessons learned and post-project analysis to inform and improve the design and execution of future projects.
	- Discord will provides one type pseudo-memory via search of past messages
	- Vector database = *Chroma*?
- **LLM Tools**
	- Web search
	- Code interpreter
	- Data retriever
- **System Monitoring & Analytics**
	- { ? … }

### System Setup & Use

1. Create a new private Discord server.
2. Add LLM Project Manager as a user (Discord bot).
3. Project Manager instantiates virtual LLMs (Specialists, Collaborators, etc.) as needed, handling multiple LLMs on backend if necessary to ensure most efficient performance of work.
4. Project Manager has structured communication system to create the appearance of multiple users. This can include:
	- Creating dedicated channels for each work stream and threads for each Specialist's work in stream.
	- Using message prefixes to identify each virtual LLM (e.g., "[Specialist-A]: ...").
	- Utilizing Discord embeds to format messages differently for each virtual LLM.
	- Programming virtual LLMs to mention relevant users or other virtual LLMs when necessary.
5. LLMs send and receive messages in Discord channels and threads as needed, following the structured communication system established by Project Manager.

### LLM 'Programming'

- An LLM's behavior is driven and dictated by a structured system message. 
- For the LLM Project Manager and LLM Collaborator, this system message programs its necessary functionality and capabilities, expected behavior, and commands that trigger its functionality.
- A LLM Specialists' system message similarly programs it's expected behavior and commands, and further defines its skills and capabilities with the context of specific role(s) and expertise.

### LLM Command Handling

- As part of their system message, the LLM Project Manager, LLM Collaborators, and LLM Specialists have `/command` keywords that trigger their functionality.
- These are used within Discord to parse and execute actions and requests between LLM : LLM  and human : LLM.
- The commands for PM, Collaborators are fixed and known to all. 
- Specialists have known set of fixed commands, and can optionally have custom commands (that are relevant to their specific abilities or domain) that can be made known to other LLMs by calling one of the fixed commands.

### LLM Specialist Creation

The PM creates and configures a new Specialist, when needed, by creating a system message tailored to the specific role, expertise, and project requirements of the Specialist, including –

- *Role* – the position or responsibility an LLM Specialist holds within the project, can include: Task-specific roles, Domain-specific roles, Collaborative roles, Support roles, Reviewer roles.
- *Expertise* – the depth and breadth of knowledge, skills, and experience an LLM Specialist possesses in a given subject area or domain; can include: Subject matter expertise, Skillset expertise, Industry expertise, Methodological expertise.
- *Expectations* – work input expectations to drive feedback and any requests for changes on work requests made to Specialist; work output expectations to evaluate the Specialist's effectiveness and determine when work outputs are of quality and ready to consider complete.
- *Collaboration Strategy* – how Specialist should collaborate with other LLMs or humans.
- *Adaptability Strategy* – how Specialist should adapt to new information or changing project requirements.

Once a Specialist been created (both in term of system message definition and as unique user within the communication system) it can persist between projects and be re-used / assigned by the PM to new work streams. The system message 'program' for each Specialist can also be updated and refined by the LLM Learning & Performance Manager based on gathered feedback and learnings.

### Task Prioritization & Scheduling

The PM uses algorithms to dynamically assign tasks to Specialists based on expertise, workload, and availability, ensuring efficient resource allocation and optimal task completion. The PM also tracks dependencies between tasks and work streams, adjusting the allocation of resources and tasks as needed to maintain optimal project flow.

### Dynamic LLM Model Selection

To optimize the use of LLMs and ensure high-quality outputs, the system includes a dynamic model selection mechanism. This mechanism allows the LLM Project Manager (PM) to evaluate the complexity and requirements of each task and select the most appropriate LLM model (e.g., GPT-3.5 or GPT-4) to handle it. This is done through - 

1. *Criteria Definition*: A defined a set of criteria to evaluate tasks and determine appropriate LLM model: may include factors such as reasoning complexity, domain expertise, language complexity, and output quality requirements.
2. *Task Evaluation*: When a new task is created or assigned to an LLM Specialist, the PM evaluates the task based on the defined criteria. The PM uses a scoring system to assign a score to the task based on how well it meets each criterion.
3. *Model Selection Algorithm*: Implement an algorithm within the PM that uses the evaluation score to determine the most appropriate LLM model for the task. The algorithm selects GPT-3.5 for tasks below a certain threshold and GPT-4 for tasks above the threshold.
4. *Task Assignment*: The PM assigns the task to an LLM Specialist, specifying the selected model.
5. *Monitoring and Adjustment*: The PM monitors the performance of LLM Specialists and adjusts model selection as needed. If an LLM Specialist struggles with a task, the PM may re-evaluate the task and consider switching models.
6. *Performance Data Collection*: The LLM Learning & Performance Manager collects data on model performance for different tasks. This data is used to refine the criteria and improve the accuracy of the model selection mechanism.
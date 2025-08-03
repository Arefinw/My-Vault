<%*
const projectBasePath = "300 Project Management/31 Active Projects";
const projectName = await tp.system.prompt("Enter Project Name:");

if (!projectName) {
    new Notice("Project creation cancelled.");
    return;
}

const projectFullPath = `${projectBasePath}/${projectName}`;

if (await this.app.vault.adapter.exists(projectFullPath)) {
    new Notice(`Error: Project "${projectName}" already exists.`);
    return;
}

try {
    // Create parent directories first
    await this.app.vault.createFolder(projectFullPath);
    await this.app.vault.createFolder(`${projectFullPath}/00 - Meta`);
    await this.app.vault.createFolder(`${projectFullPath}/10 - Planning`);
    const executionPath = `${projectFullPath}/20 - Execution`;
    await this.app.vault.createFolder(executionPath);
    const resourcesPath = `${projectFullPath}/30 - Resources`;
    await this.app.vault.createFolder(resourcesPath);
    const reviewPath = `${projectFullPath}/40 - Review & Reporting`;
    await this.app.vault.createFolder(reviewPath);
    const deliverablesPath = `${projectFullPath}/50 - Deliverables`;
    await this.app.vault.createFolder(deliverablesPath);
    await this.app.vault.createFolder(`${projectFullPath}/99 - Archive`);

    // Create nested directories
    await this.app.vault.createFolder(`${executionPath}/21 - Tasks`);
    await this.app.vault.createFolder(`${executionPath}/22 - Meeting Notes`);
    await this.app.vault.createFolder(`${executionPath}/23 - Work in Progress`);
    await this.app.vault.createFolder(`${executionPath}/24 - Correspondence`);
    await this.app.vault.createFolder(`${resourcesPath}/31 - Source Material`);
    await this.app.vault.createFolder(`${resourcesPath}/32 - Research & Inspiration`);
    await this.app.vault.createFolder(`${reviewPath}/41 - Progress Reports`);
    await this.app.vault.createFolder(`${reviewPath}/42 - Retrospectives & Lessons Learned`);
    await this.app.vault.createFolder(`${deliverablesPath}/51 - Drafts`);
    await this.app.vault.createFolder(`${deliverablesPath}/52 - Final`);

    // Create placeholder files with tags
    const fileContent = (tags, title = "") => `${tags}\n\n# ${title}`;
    await this.app.vault.create(`${projectFullPath}/00 - Meta/01 - Brief & Scope.md`, fileContent("#p/project/active\n#s/project/personal", projectName));
    await this.app.vault.create(`${projectFullPath}/00 - Meta/02 - Stakeholders & Roles.md`, fileContent("#t/project/meta"));
    await this.app.vault.create(`${projectFullPath}/00 - Meta/03 - Goals & Success Criteria.md`, fileContent("#t/project/meta"));
    await this.app.vault.create(`${projectFullPath}/00 - Meta/04 - Project Journal.md`, fileContent("#t/project/meta"));
    await this.app.vault.create(`${projectFullPath}/10 - Planning/11 - Roadmap & Milestones.md`, fileContent("#t/project/planning"));
    await this.app.vault.create(`${projectFullPath}/10 - Planning/12 - Timeline & Schedule.md`, fileContent("#t/project/planning"));
    await this.app.vault.create(`${projectFullPath}/10 - Planning/13 - Risk Assessment.md`, fileContent("#t/project/planning"));
    await this.app.vault.create(`${projectFullPath}/10 - Planning/14 - Communication Plan.md`, fileContent("#t/project/planning"));
    await this.app.vault.create(`${projectFullPath}/30 - Resources/33 - Tools & Credentials.md`, fileContent("#t/project/resource"));

    new Notice(`Project "${projectName}" created successfully!`);
} catch (error) {
    new Notice(`Error creating project: ${error}`);
    console.error(error);
}
%>

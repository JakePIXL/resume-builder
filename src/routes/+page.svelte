<!-- src/routes/resume/+page.svelte -->
<script lang="ts">
	import { env } from "$env/dynamic/public";

    // Resume data interfaces
    interface Skill {
      name: string;
      category: 'technical' | 'soft' | 'tools';
    }
  
    interface Experience {
      title: string;
      company: string;
      location: string;
      startDate: string;
      endDate: string;
      points: string[];
    }
  
    interface Project {
      name: string;
      description: string;
      technologies: string[];
      link?: string;
    }
  
    interface Education {
      degree: string;
      school: string;
      location: string;
      graduation: string;
      details?: string[];
    }
  
    // Your resume data
    const personalInfo = {
      name: "Your Name",
      title: "Backend Developer & Security Specialist",
      email: "your.email@example.com",
      phone: "(555) 555-5555",
      location: "Your Location",
      github: "github.com/yourusername",
      linkedin: "linkedin.com/in/yourusername"
    };
  
    const skills: Skill[] = [
      { name: "Rust", category: "technical" },
      { name: "SvelteKit", category: "technical" },
      { name: "Cybersecurity", category: "technical" },
      { name: "Network Security", category: "technical" },
      { name: "Educational Technology", category: "technical" }
    ];
  
    const experience: Experience[] = [
      {
        title: "Senior Backend Developer",
        company: "Company Name",
        location: "Location",
        startDate: "2022",
        endDate: "Present",
        points: [
          "Developed secure microservices using Rust",
          "Implemented educational platforms using SvelteKit",
          "Led security audits and penetration testing initiatives"
        ]
      }
    ];
  
    const projects: Project[] = [
      {
        name: "Example",
        description: "Secure exanoke management system built with Rust and SvelteKit",
        technologies: ["Rust", "SvelteKit", "TailwindCSS"],
        link: "example.com/example"
      }
    ];
  
    const education: Education[] = [
      {
        degree: "Bachelor's in Cybersecurity",
        school: "University Name",
        location: "Location",
        graduation: "2022",
        details: ["Relevant coursework", "Notable achievements"]
      }
    ];
  </script>
  
  <svelte:head>
    <title>{personalInfo.name} - Resume</title>
    <link rel="stylesheet" href={env.PUBLIC_FONT_URL}>
    <style>
      @font-face {
        font-family: "TX-02", monospace;
        font-weight: normal;
        font-style: normal;
      }
  
      @media print {
        @page {
          margin: 2.54cm;
          size: letter portrait;
        }
  
        body {
          -webkit-print-color-adjust: exact !important;
          print-color-adjust: exact !important;
        }
  
        a {
          text-decoration: none !important;
          color: inherit !important;
        }
      }
    </style>
  </svelte:head>
  
  <div class="mx-auto max-w-4xl p-8 print:p-0 font-['TX-02']">
    <!-- Header -->
    <header class="mb-8">
      <h1 class="text-3xl font-bold mb-2">{personalInfo.name}</h1>
      <p class="text-xl mb-4">{personalInfo.title}</p>
      <div class="flex flex-wrap gap-4 text-sm">
        <span>📧 {personalInfo.email}</span>
        <span>📱 {personalInfo.phone}</span>
        <span>🔗 {personalInfo.github}</span>
        <span>📍 {personalInfo.location}</span>
      </div>
    </header>
  
    <!-- Skills -->
    <section class="mb-8">
      <h2 class="text-xl font-bold mb-4 pb-1 border-b-2 border-gray-800">
        Technical Skills
      </h2>
      <div class="flex flex-wrap gap-2">
        {#each skills as skill}
          <span class="bg-gray-200 px-2 py-1 rounded-md text-sm">
            {skill.name}
          </span>
        {/each}
      </div>
    </section>
  
    <!-- Experience -->
    <section class="mb-8">
      <h2 class="text-xl font-bold mb-4 pb-1 border-b-2 border-gray-800">
        Professional Experience
      </h2>
      {#each experience as job}
        <div class="mb-6">
          <h3 class="font-bold">{job.title}</h3>
          <p class="text-sm text-gray-600">
            {job.company} • {job.location} • {job.startDate} - {job.endDate}
          </p>
          <ul class="list-disc ml-4 mt-2 text-sm">
            {#each job.points as point}
              <li>{point}</li>
            {/each}
          </ul>
        </div>
      {/each}
    </section>
  
    <!-- Projects -->
    <section class="mb-8">
      <h2 class="text-xl font-bold mb-4 pb-1 border-b-2 border-gray-800">
        Notable Projects
      </h2>
      {#each projects as project}
        <div class="mb-6">
          <h3 class="font-bold">{project.name}</h3>
          <p class="text-sm mt-2">{project.description}</p>
          <div class="flex flex-wrap gap-2 mt-2">
            {#each project.technologies as tech}
              <span class="bg-gray-200 px-2 py-1 rounded-md text-sm">
                {tech}
              </span>
            {/each}
          </div>
          {#if project.link}
            <a href={project.link} class="text-sm text-gray-600 mt-1 block">
              {project.link}
            </a>
          {/if}
        </div>
      {/each}
    </section>
  
    <!-- Education -->
    <section class="mb-8">
      <h2 class="text-xl font-bold mb-4 pb-1 border-b-2 border-gray-800">
        Education
      </h2>
      {#each education as edu}
        <div class="mb-4">
          <h3 class="font-bold">{edu.degree}</h3>
          <p class="text-sm text-gray-600">
            {edu.school} • {edu.location} • {edu.graduation}
          </p>
          {#if edu.details}
            <ul class="list-disc ml-4 mt-2 text-sm">
              {#each edu.details as detail}
                <li>{detail}</li>
              {/each}
            </ul>
          {/if}
        </div>
      {/each}
    </section>
  </div>
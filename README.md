# Oculife
Oculife was created during [TreeHacks 2024](https://www.treehacks.com/) at Stanford University.
The following content is available on [Devpost](https://devpost.com/software/oculife) as well.

## Inspiration
We were inspired to address the critical issue of mitigating delays in accessing emergency medical services. Every year, more than 500,000 maternal deaths occur, with 95% of these in low-income countries where emergency care is often lacking [1]. The average response time for ambulances in developing countries is 60 to 80 minutes; sudden cardiac arrest can be fatal if it lasts longer than eight minutes without CPR [2] [3].

This project was also in part inspired by Brandon, a contributor to our project, when he experienced a first-hand situation where Oculife would have been applicable. During one of his speed skating competitions, his left middle and ring fingers were lacerated, resulting in 100% and 80% lacerations of the tendons in those two fingers. The competition medical staff wasn’t effectively trained in treating deep cuts, resulting in severe consequences and complications to this day. Timely administration of medical procedures would have improved the result of the surgery’s rehabilitation process.

## What it does
Oculife saves precious time, allowing for immediate action to save lives instead of searching through ad-infested, SEO-targeted spam content for symptoms when time is critical.

Oculife is a pioneering XR application that uses audio input to generate medical instructions and syncs with video demonstrations for emergency aid procedures. It currently supports emergency medical guidance for seven common conditions and general emergency care, empowering non-medically trained personnel to accurately and readily administer life-saving procedures in a life-threatening situation.

Oculife is currently implemented as a visionOS client to leverage one of XR's strengths: displaying large screens directly in front of you. This setup allows you to follow a step-by-step tutorial right in front of the patient, eliminating the need to squint at your phone. XR headsets are not yet widely accessible, but Oculife can be easily ported to existing mobile platforms like iOS, as it is developed in Swift.

### Emergency Assistance
When emergency assistance mode is engaged, Oculife will take in an audio recording of the user describing the emergency situation, similar to how they would describe the situation to a first responder. It then uses speech-to-text translation and uses a large language model to perform a classification task of the audio description. Based on that classification, Oculife will display an emergency guidance screen in extended reality. The emergency guidance screen contains both a video walkthrough and step-by-step instructions of the necessary steps to treat the patient.

### Training Assistance
When training assistance mode is engaged, Oculife provides users with various medical condition options to learn about the treatment an individual can employ. Based on the user’s selection on the application, Oculife will display a video walkthrough and step-by-step instructions specifically for that medical condition to teach users what actions to take and the practice necessary to be prepared for a real emergency situation.

## How we built it
- Client
    - Language: Swift
    - Runtime: visionOS
    - Transforms Speech-to-Text with built-in `SpeechRecognizer`
    - Includes Alamofire to make HTTP requests
    - Uses a custom video player that syncs with the medical instruction timestamps in order to show animated step-by-step instructions
    - XR interactions are mostly compatible with existing SwiftUI code, but special design considerations to make the UI most fitting to an AR environment was taken
        - Windows are movable and resizable
        - Video is prominent
        - Less complexity within the UI that speeds up user navigation
- Server
    - Language: Python
    - Exposes HTTP APIs to communicate with the client
    - Uses a customized Mistral AI chat completions model that runs on Together.ai to process speech, categorize symptoms, and generate solutions
    - Does an in-memory lookup to identify symptoms with pre-processed solutions and videos or if missing, uses the LLM to generate solutions on-the-fly 
    - Maintains prompt history in order to provide relevant context
    - Debugged API endpoints using Postman

## Challenges we ran into
visionOS is an all-new mixed-reality operating system so it was challenging to build Oculife due to the lack of resources and prior implementation. A lot of time had to be spent examining the raw Swift documentation throughout the development process. We were also challenged to fine-tune a state-of-the-art open-source large language model, Mistral, to perform classification tasks on different emergency medical conditions reliably without producing hallucinations.

## Accomplishments that we're proud of
We’re proud of our unwavering commitment and grit. All of us were new to the platforms that we were focusing on. This was Andrew and Brandon’s first Python backend server and Taeuk’s first visionOS application, and we’re happy how much we were able to accomplish in a short while! We’re also proud of creating an application that expands the accessibility of healthcare services and the well-being of others—two goals that are deeply important to us. Finally, we are also proud to build for emerging technologies like XR and create forward-looking and innovative applications.

## What we learned
This project brought to light the disparity of access to first-aid emergency care in different geographical areas and the limitations it can place on an individual’s life. We learned the impact that can be made by leveraging emerging technologies in order to address these disparities. Through pioneering, innovative solutions, we can improve healthcare for those in developing countries.

We learned to collaborate effectively and problem solve to create an innovative prototype, all under tight time constraints. We were also able to meet other developers, mentors, and like-minded thinkers who share in our passion to develop more comprehensive healthcare solutions. Our discussions about the future of XR technology and app development on these platforms continues to inform our inspiration and design for new products even after this hackathon.

## What's next for Oculife
We plan to continue iterating on the current version of Oculife and developing new features after TreeHacks. With the popularization and expansion of telehealth in recent years, we consider real-time consultations and guidance with medical professionals through video conferencing as a driver to enhance the efficacy of Oculife. We also plan to expand our medical conditions database, ensuring a more comprehensive coverage of emergency aid. For expanded access to our app, we plan to implement language translation support. Finally, implementing adaptive AI for education and providing certifications through our training module will provide a significant value-add to professionals seeking licensure.

## References
[1] Jamison. Disease Control Priorities in Developing Countries (2nd Edition). The World Bank Group, 2006.

[2] “How Can We Get Patients in Developing Countries to Hospital Faster?” World Economic Forum, www.weforum.org/agenda/2015/12/how-can-we-get-patients-in-developing-countries-to-hospital-faster/. Accessed 18 Feb. 2024.

[3] Cleveland Clinic medical. “What Is Cardiac Arrest?” Cleveland Clinic, my.clevelandclinic.org/health/diseases/21736-cardiac-arrest. Accessed 18 Feb. 2024.

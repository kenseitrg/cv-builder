<script>
    import { Form } from "sveltestrap";
    import Bio from "./form-parts/Bio.svelte";
    import Contacts from "./form-parts/Contacts.svelte";
    import Profile from "./form-parts/Profile.svelte";
    import Education from "./form-parts/Education.svelte";
    import Experience from "./form-parts/Experience.svelte";
    import { createEventDispatcher } from "svelte";

    export let cvInfo = {
        bio: {},
        contacts: {},
        profile: "",
        education: [],
        experience: [],
    };
    const dispatch = createEventDispatcher();

    const handleBio = (event) => {
        event.preventDefault();
        cvInfo.bio = event.detail;
        dispatch("form-changed", cvInfo);
    };

    const handleContacts = (event) => {
        event.preventDefault();
        cvInfo.contacts = event.detail;
        dispatch("form-changed", cvInfo);
    };

    const handleProfile = (event) => {
        event.preventDefault();
        cvInfo.profile = event.detail;
        dispatch("form-changed", cvInfo);
    };

    const handleEducation = (event) => {
        event.preventDefault();
        cvInfo.education = event.detail;
        dispatch("form-changed", cvInfo);
    };

    const handleExperience = (event) => {
        event.preventDefault();
        cvInfo.experience = event.detail;
        dispatch("form-changed", cvInfo);
    };
</script>

<Form>
    <Bio on:bio-changed={handleBio} />
    <Contacts on:contacts-changed={handleContacts} />
    <Profile on:profile-changed={handleProfile} />
    <Education on:education-changed={handleEducation} />
    <Experience on:experience-changed={handleExperience} />
</Form>

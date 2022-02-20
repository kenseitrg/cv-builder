<script>
    import {
        Card,
        CardBody,
        CardHeader,
        Col,
        Container,
        Input,
        Label,
        Row,
        Button,
        Collapse,
        Icon,
    } from "sveltestrap";

    import { createEventDispatcher } from "svelte";

    export let bio = {
        firstName: "",
        lastName: "",
        title: "",
    };

    const dispatch = createEventDispatcher();

    const handleChange = (event) => {
        event.preventDefault();
        bio = bio;
        dispatch("bio-changed", bio);
    };
</script>

<Card class="mb-1">
    <CardHeader>
        <Container fluid>
            <Row>
                <Col>
                    <p>Bio</p>
                </Col>
                <Col xs="auto">
                    <Button outline id="togglerBio">
                        <Icon name="three-dots" />
                    </Button>
                </Col>
            </Row>
        </Container>
    </CardHeader>
    <Collapse toggler="#togglerBio">
        <CardBody>
            <Container fluid>
                <Row>
                    <Col>
                        <Label for="firstName">First name</Label>
                        <Input
                            type="text"
                            name="firstName"
                            id="firstName"
                            placeholder="First name"
                            bind:value={bio.firstName}
                            on:change={handleChange}
                        />
                    </Col>
                    <Col>
                        <Label for="lastName">Last name</Label>
                        <Input
                            type="text"
                            name="lastName"
                            id="lastName"
                            placeholder="Last name"
                            bind:value={bio.lastName}
                            on:change={handleChange}
                        />
                    </Col>
                </Row>
                <Row>
                    <Col>
                        <Label for="jobTitle">Job title</Label>
                        <Input
                            type="text"
                            name="jobTitle"
                            id="jobTitle"
                            placeholder="Job title"
                            bind:value={bio.title}
                            on:change={handleChange}
                        />
                    </Col>
                </Row>
            </Container>
        </CardBody>
    </Collapse>
</Card>

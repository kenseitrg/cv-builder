<script>
    import { validate_component } from "svelte/internal";

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

    const dispatch = createEventDispatcher();

    let jobList = [];

    const handleRemove = (event, job) => {
        event.preventDefault();
        jobList = jobList.filter((el) => el.id != job);
        dispatch("experience-changed", jobList);
    };

    const handleAdd = (event) => {
        event.preventDefault();
        jobList.push({
            id: new Date().getTime() & 0xffff,
            start: "",
            end: "",
            place: "",
            description: "",
        });
        jobList = jobList;
        dispatch("experience-changed", jobList);
    };

    const handleChange = (event) => {
        event.preventDefault();
        jobList = jobList;
        dispatch("experience-changed", jobList);
    };
</script>

<Card class="mb-1">
    <CardHeader>
        <Container fluid>
            <Row>
                <Col>
                    <p>Work experience</p>
                </Col>
                <Col xs="auto">
                    <Button outline id="togglerWork">
                        <Icon name="three-dots" />
                    </Button>
                </Col>
            </Row>
        </Container>
    </CardHeader>
    <Collapse toggler="#togglerWork">
        <CardBody class="border">
            <Container fluid>
                {#each jobList as job}
                    <div class="border mb-3">
                        <Row>
                            <Col>
                                <Label for="startWork{job.id}">Start</Label>
                                <Input
                                    type="date"
                                    name="startWork{job.id}"
                                    id="startWork{job.id}"
                                    placeholder=""
                                    bind:value={job.start}
                                    on:change={handleChange}
                                />
                            </Col>
                            <Col>
                                <Label for="endWork{job.id}">End</Label>
                                <Input
                                    type="date"
                                    name="endWork{job.id}"
                                    id="endWork{job.id}"
                                    placeholder=""
                                    bind:value={job.end}
                                    on:change={handleChange}
                                />
                            </Col>
                            <Col xs="auto">
                                <Button
                                    outline
                                    id="removeWork{job.id}"
                                    on:click={(event) =>
                                        handleRemove(event, job.id)}
                                >
                                    <Icon name="trash" />
                                </Button>
                            </Col>
                        </Row>
                        <Row>
                            <Col>
                                <Label for="workPlace{job.id}"
                                    >Company Name</Label
                                >
                                <Input
                                    type="text"
                                    name="workPlace{job.id}"
                                    id="workPlace{job.id}"
                                    placeholder="ACME_{job.id} Inc."
                                    bind:value={job.place}
                                    on:change={handleChange}
                                />
                            </Col>
                        </Row>
                        <Row>
                            <Col>
                                <Label for="workResp{job.id}"
                                    >Job description</Label
                                >
                                <Input
                                    type="textarea"
                                    name="workDesc{job.id}"
                                    id="workDesc{job.id}"
                                    placeholder="Job description"
                                    bind:value={job.description}
                                    on:change={handleChange}
                                />
                            </Col>
                        </Row>
                    </div>
                {/each}
                <Row class="justify-content-center">
                    <Col class="justify-content-center">
                        <Button outline id="addWork" on:click={handleAdd}>
                            <Icon name="plus-circle" />
                        </Button>
                    </Col>
                </Row>
            </Container>
        </CardBody>
    </Collapse>
</Card>

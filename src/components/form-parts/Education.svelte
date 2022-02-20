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

    const dispatch = createEventDispatcher();

    let eduList = [];

    const handleRemove = (event, job) => {
        event.preventDefault();
        eduList = eduList.filter((el) => el.id != job);
        dispatch("education-changed", eduList);
    };

    const handleAdd = (event) => {
        event.preventDefault();
        eduList.push({
            id: new Date().getTime() & 0xffff,
            start: "",
            end: "",
            place: "",
            degree: "",
        });
        eduList = eduList;
        dispatch("education-changed", eduList);
    };

    const handleChange = (event) => {
        event.preventDefault();
        eduList = eduList;
        dispatch("education-changed", eduList);
    };
</script>

<Card class="mb-1">
    <CardHeader>
        <Container fluid>
            <Row>
                <Col>
                    <p>Education</p>
                </Col>
                <Col xs="auto">
                    <Button outline id="togglerEdu">
                        <Icon name="three-dots" />
                    </Button>
                </Col>
            </Row>
        </Container>
    </CardHeader>
    <Collapse toggler="#togglerEdu">
        <CardBody>
            <Container fluid>
                {#each eduList as place}
                    <div class="border mb-3">
                        <Row>
                            <Col>
                                <Label for="startEdu{place.id}">Start</Label>
                                <Input
                                    type="date"
                                    name="startEdu{place.id}"
                                    id="startEdu{place.id}"
                                    placeholder=""
                                    bind:value={place.start}
                                    on:change={handleChange}
                                />
                            </Col>
                            <Col>
                                <Label for="endEdu{place.id}">End</Label>
                                <Input
                                    type="date"
                                    name="endEdu{place.id}"
                                    id="endEdu{place.id}"
                                    placeholder=""
                                    bind:value={place.end}
                                    on:change={handleChange}
                                />
                            </Col>
                            <Col xs="auto">
                                <Button
                                    outline
                                    id="removeWork{place.id}"
                                    on:click={(event) =>
                                        handleRemove(event, place.id)}
                                >
                                    <Icon name="trash" />
                                </Button>
                            </Col>
                        </Row>
                        <Row>
                            <Col>
                                <Label for="eduPlace{place.id}"
                                    >University Name</Label
                                >
                                <Input
                                    type="text"
                                    name="eduPlace{place.id}"
                                    id="eduPlace{place.id}"
                                    placeholder="University of Pittsburgh"
                                    bind:value={place.place}
                                    on:change={handleChange}
                                />
                            </Col>
                        </Row>
                        <Row>
                            <Col>
                                <Label for="eduDegree{place.id}"
                                    >Degree Name</Label
                                >
                                <Input
                                    type="text"
                                    name="eduDegree{place.id}"
                                    id="eduDegree{place.id}"
                                    placeholder="B.S in Computer Science"
                                    bind:value={place.degree}
                                    on:change={handleChange}
                                />
                            </Col>
                        </Row>
                    </div>
                {/each}
                <Row class="justify-content-center">
                    <Col class="justify-content-center">
                        <Button outline id="addEdu" on:click={handleAdd}>
                            <Icon name="plus-circle" />
                        </Button>
                    </Col>
                </Row>
            </Container>
        </CardBody>
    </Collapse>
</Card>

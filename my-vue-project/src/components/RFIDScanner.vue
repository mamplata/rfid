<template>
    <div class="bg-light text-dark">
        <div class="header d-flex justify-content-between align-items-center py-3" style="background-color: #198754; color: white;">
            <div class="d-flex flex-column justify-content-center align-items-center">
                <h1 class="display-3">iAttend</h1>
                <h2>RFID Attendance System</h2>
            </div>
            <button class="btn btn-light">Logout</button>
        </div>

        <div class="head-section d-flex flex-column align-items-center bg-light text-dark p-5" style="background-image: url('https://www.toptal.com/designers/subtlepatterns/patterns/diagmonds.png'); background-size: cover; color: white;">
            <h1 class="display-3">Wednesday, Wash Day</h1>
            <h3 class="text-muted">The day where students can wash their clothes</h3>
            <div class="pt-3">
                <strong>Current Time:</strong> <!-- Add dynamic time here -->
            </div>
        </div>

        <div class="main d-flex flex-column flex-lg-row">
            <!-- Left Column (Scanner with Animation) -->
            <div class="col-12 col-lg-5 p-4" style="background-color: #F6F7FB;">
                <div class="scanner-tag">
                    <!-- Insert scanner tag with animation here -->
                    <!-- For example, you can add an animated GIF or CSS animation -->
                    <img src="../assets/img/scanner-animation.gif" alt="Scanner Animation" class="w-100" />
                </div>
            </div>

            <!-- Right Column (Attendance Table) -->
            <div class="col-12 col-lg-7 p-4" style="background-color: #F6F7FB;">
                <h3 class="text-center text-dark">Latest Attendance</h3>
                <!-- Example Table for Latest 5 Attendance -->
                <table class="table table-striped">
                    <thead class="table-dark">
                        <tr>
                            <th>#</th>
                            <th>Name</th>
                            <th>Time</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr>
                            <td>1</td>
                            <td>John Doe</td>
                            <td>10:30 AM</td>
                        </tr>
                        <tr>
                            <td>2</td>
                            <td>Jane Smith</td>
                            <td>10:35 AM</td>
                        </tr>
                        <tr>
                            <td>3</td>
                            <td>Sam Wilson</td>
                            <td>10:40 AM</td>
                        </tr>
                        <tr>
                            <td>4</td>
                            <td>Amy Lee</td>
                            <td>10:45 AM</td>
                        </tr>
                        <tr>
                            <td>5</td>
                            <td>Peter Parker</td>
                            <td>10:50 AM</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            msg: 'hello world'
        }
    },
    computed: {
    },
    methods: {
    }
}
</script>

<style scoped>
/* Custom Styles for Applying the 60-30-10 Rule */
.bg-light {
    background-color: #F6F7FB !important; /* 60% */
}

.text-dark {
    color: #212121 !important; /* 10% */
}

.header {
    background-color: #198754 !important; /* 30% */
}

.text-muted {
    color: #6c757d !important;
}

.table-dark {
    background-color: #198754 !important;
}

.table-dark th,
.table-dark td {
    color: white !important;
}
</style>

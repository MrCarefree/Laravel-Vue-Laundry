<template>
    <!-- Content Header (Page header) -->
    <div class="content-header">
        <div class="container-fluid">
            <div class="row mb-2">
                <div class="col-sm-6">
                    <h1 class="m-0 text-dark">{{ title }}</h1>
                </div>
                <!-- /.col -->
                <div class="col-sm-6">
                    <ol class="breadcrumb float-sm-right">
                        <li class="breadcrumb-item" v-for="parent in breadcumb.parent">
                            <a href="#">{{ parent }}</a>
                        </li>
                        <li class="breadcrumb-item active">{{ breadcumb.active }}</li>
                    </ol>
                </div>
                <!-- /.col -->
            </div>
            <!-- /.row -->
        </div>
        <!-- /.container-fluid -->
    </div>
    <!-- /.content-header -->
</template>

<script>
    export default {
        props: {
            title: {
                type: String,
                required: true
            },
            breadcumb: {
                type: Object,
                required: true
            }
        }
    };
</script>
